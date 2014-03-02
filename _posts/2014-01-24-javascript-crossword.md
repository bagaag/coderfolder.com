---
layout: post
title: "Browser-based crossword puzzle implemented in JavaScript"
tags: javascript games project
---

This is a browser-based crossword puzzle game implemented completely in JavaScript. I wrote this sometime last summer. Some of its features:

* Reads in the puzzle data as json from a separate .js file. <a href="https://github.com/wiseley/javascript-crossword/blob/master/puzzle.js">Here's what it looks like</a>. To be honest, I don't recall where the sample clues came from, but I know they're not mine.
* The entire puzzle can be navigated using the keyboard. Try tab, shift+tab and the arrow keys.
* It supports multiple puzzles on the page and can be directed at any HTML container. 
* It saves the puzzle state in a cookie so your hard work will survive a browser crash or accidental URL change.

The code is available at <a href="https://github.com/wiseley/javascript-crossword/">github.com/wiseley/javascript-crossword</a>.

Here it is in an IFRAME:

<iframe height="530" width="700" src="/projects/javascript-crossword/index.html" style="border:none"></iframe>


