---
layout: post
title: A palindrome test function in JavaScript
tags: kata javascript
---

We gave this test at some dev interviews today: write a function that returns true if the word passed to it is a palindrome (the same backwards as forwards) or false if not. 

The 2nd solution here is what first came to mind when solving this on my own, but I must admit, rusty as I am, I struggled a bit with the +/-1 of finding the middle character of a word like 'mom' and how to handle a word like 'toot' that has no middle character. I probably would have botched this part under the stress of an interview, especially checking for the b<a, which only came to me after debugging it. Then it occurred to me the simplest solution is to just reverse the word and compare it with the original. I have both options here.

{% highlight javascript %}
// reverse and compare
function isPalindrome1(word) {
    var s = '';
    for (var i=word.length-1; i>=0; i--) {
	    s += word[i];
    }
    return s === word;
}

// compare characters from end to end (more efficient)
function isPalindrome2(word) {
    for (var a=0; a<word.length; a++) {
	    var b = word.length-1 - a;
	    if (a===b || b<a) return true;
	    else if (word[a]!=word[b]) return false;
    }
}
{% endhighlight %}

[See the code in GitHub](https://gist.github.com/wiseley/8611619)

Now here's a good interview question: Why is the second implementation more efficient? 
