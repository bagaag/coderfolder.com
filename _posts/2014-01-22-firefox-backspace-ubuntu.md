---
layout: post
title: "Make the Backspace key work in Firefox on Ubuntu"
tags: ubuntu
---

Another Ubuntu oddity. Who doesn't use the Backspace key to go back in their browser? The Ubuntu users at Firefox, apparently.

Thanks to [this post](http://embraceubuntu.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/) for filling me in on the fix. It provides the back story (yes, there is a reason, if not a good one). But in case that goes away, here's the payoff:

Type "about:config" in the address bar of Firefox and press Enter. Search for `browser.backspace_action` and change its value to 0 (zero).
