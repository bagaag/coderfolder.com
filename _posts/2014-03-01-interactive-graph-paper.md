---
layout: post
title: A Graph Paper SVG Drawing App
tags: javascript svg project
---

This is a simple graph paper drawing app implemented in JavaScript and SVG. The idea came to me while planning out large structures in Minecraft. I've always wanted to learn about coding SVG in the browser and this was a fun way to do that. In addition to jQuery, of course, it uses:

* <a href="http://bgrins.github.io/spectrum/">Spectrum, The No Hassle jQuery Colorpicker</a> - This is just the color picker; I coded the eye dropper functionality.
* <a href="http://snapsvg.io/">Snap, a JavaScript SVG library</a> - Apparently jQuery's native handling of SVG tags is a little shaky, so this provides programmatic creation of elements, event handlers, etc.

The code is available at <a href="https://github.com/wiseley/graph-paper/">github.com/wiseley/graph-paper/</a>.

Here it is in an IFRAME:

<iframe height="450" width="700" src="/projects/graph-paper/index.html" style="border:none"></iframe>


If the mood strikes I may add a few features that would make it more useful:

* Cookie persistence of the drawing
* Zooming in and out
