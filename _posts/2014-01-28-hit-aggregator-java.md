---
layout: post
title: "Hit Aggregator Programming Problem"
tags: java, kata, interviews
---

This programming problem came to me through an interview some time ago. Maybe I'm slow, but it's not the type of problem I can solve in 10-15 minutes under the stress of an interview and coding on a whiteboard. I didn't get the job, but I did go home and solve the problem on my own - for fun. I ended up spending a couple hours coding it after mulling over the problem for an afternoon during the course of other activities. It's an interesting data structure problem.

Here it is:

> Write a class to support the following website feature. On each product detail page, display the number of hits in the past 10 minutes if there have been at least 10. Otherwise, display the number of hits in the past hour if there have been at least 10. Otherwise, display the 
number of hits in the past 24 hours if there have been at least 10. Otherwise, display nothing. There is no analytics service available to provide realtime reporting on the number of hits, so this class must also collect that data. It should aim to work on a website that has a few million product pages and gets 10 million unique visitors per day.

Some observations I had on the problem:

* How the heck do I collect that much data and report on it in real time? The load requirements of the site preclude just inserting database records for each hit and querying that data, and storing the data in memory would also be impractical. 
* We only care about 24 hours, so anything collecting the data also needs to prune it. 
* The data needs to be stored in aggregate form. Hits could be grouped into 1 minute increments and still support the required functionality. It's tempting to think that storing the counts in 10 minute groups would work given the requirements, but 1 minute intervals are needed as "the last 10 minutes" changes every minute.
* The fact that we only need a threshold that exceeds 10 hits means we don't need to look at the entire data set for each hit as long as we sort it by descending date.

The algorithm I came up with goes something like this:

* Get the list of dated hit counts for the current page. These are kept in a list of per-minute hit counts keyed by page.
* Record a hit for the current page in the appropriately dated hit count. Recording the hit and reporting the statistic happen in a single call. 
* Traverse the hits in reverse chronological order, counting as we go.
* Before exceeding the current time threshold (10 min, 1 hr, 24 hrs), check to see if we've exceeded the minimum hit threshold (10), and get out if we have.
* Prune hit counts beyond the minimum threshold that meets the minimum number of hits.

One improvement I might make is to replace the index-based iteration (`for (int i=counts.size()-1; i>=0; i-- )`) with an iterator, allowing us to swap out the implementation of that List if needed with one that doesn't support index-based access. That would require a backwards iterator, which Java doesn't provide out of the box. There's a <a href="http://stackoverflow.com/questions/2102499/iterating-through-a-list-in-reverse-order-in-java">post on Stackoverflow</a> showing how this can be done.

Here's my full solution:

~~~ java
import java.util.*;

public class HitAggregator {

	// 10 min, 1 hr, 24 hr
	private final static int[] THRESHOLDS = {10, 60, 1440};

	// number of hits needed to satisfy a threshold
	private final static int MIN_HITS = 10;

	// stores a list of dated hits for each id
	private Map<Long,List<Entry>> hitCounts = new HashMap<Long,List<Entry>>();

	// dated hit count, hits are grouped for 1 minute
	protected static final class Entry {
		public long date = System.currentTimeMillis(); 
		public int hits = 1;
	}

	// return value must include the hit count and the threshold
	public static final class Result {
		public int threshold; // in minutes (10 min, 1hr, 24 hr)
		public int hits; // number of hits
		public Result(int t, int h) { threshold = t; hits = h; }
	}

	// get list of minute/counts for an id
	private List<Entry> getCounts(long id) {
		List<Entry> counts = this.hitCounts.get(id);
		if (counts==null) {
			counts = new ArrayList<Entry>();
			this.hitCounts.put(id, counts);
		}
		return counts;
	}

	// record a hit
	private void recordHit(List<Entry> counts, long id, long now) {
		long minuteAgo = now - (60*1000);

		// get most recent entry and add to it if it's for the current minute, 
        // or create a new one
		Entry latest = null;
		if (counts.size()>0) {
			// get latest entry
			latest = counts.get(counts.size()-1);
			// increment if its for this minute
			if (latest.date > minuteAgo) {
				latest.hits++;
			} 
			else {
				// minute has passed, create hit count for the current minute
				counts.add(new Entry());
			}
		} 
		else {
			// empty list, create new hit count
			counts.add(new Entry());
		}
	}

	/* record a hit for the page and return a result object */
	/* this is the only method exposed to the servlet layer */
	public Result aggregate(long id) {

		// get entry list for this id
		List<Entry> counts = getCounts(id);

		// record the hit
		long now = System.currentTimeMillis();
		recordHit(counts, id, now);

		// get the hit count and threshold
		int hits = 0;
		int threshold_ix = 0;
		int threshold = HitAggregator.THRESHOLDS[threshold_ix];
		long threshold_date = now - (threshold*60*1000);
		// walk through the hit counts backwards
		for (int i=counts.size()-1; i>=0; i-- ) {
			Entry e = counts.get(i);
			// increment hits if within the current threshold
			if (e.date > threshold_date) {
				hits += e.hits;
			}
			// we've met the min threshold hits, so get out
			else if (hits >= HitAggregator.MIN_HITS) {
				counts.subList(0,i).clear(); // had to look up this trick
				break;
			}
			// increase threshold to look for more hits
			else {
				threshold_ix++;
				if (HitAggregator.THRESHOLDS.length <= threshold_ix) {
					threshold = HitAggregator.THRESHOLDS[threshold_ix];
					threshold_date = now - (threshold*60*1000);
				}
				// out of HitAggregator.THRESHOLDS, remove old entries and get out
				else {
					counts.subList(0,i).clear(); 
					break;
				}
			}
		}
		// return result or null if we don't have the minimum hits needed 
		Result result = null;
		if (hits >= HitAggregator.MIN_HITS) {
			result = new Result(threshold, hits);
		}
		return result;
	}
}
~~~
