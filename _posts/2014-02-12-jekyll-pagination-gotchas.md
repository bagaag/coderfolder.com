---
layout: post
title: How to get Pagination working in Jekyll
tags: jekyll
---

While reading through the <a href="http://jekyllrb.com/docs/pagination/">Jekyll documentation on Pagination</a>, I thought I'd give it a go on this site.

After banging my head for a little while, I noticed the giant blue notice on that page telling me that it only works in HTML files. Duh. That's not news.

But then, after changing my file to HTML, banged on my head for a LONG time. It just wouldn't work. Finally, on a hunch, I ran `jekyll build`. Bam, it worked. 

I was running `jekyll serve -w` and testing my changes locally. Apparently this doesn't *really* build the site when a file changes. Not sure exactly what it does, but at least as far as Pagination goes, it doesn't build.

