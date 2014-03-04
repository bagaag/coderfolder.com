---
layout: post
title: Bootswatch Superhero
tags: bootstrap
---

I just installed the Bootswatch <a href="http://bootswatch.com/superhero/">Superhero</a>  theme on this site. The only tweaks I made were `body { font-weight: 400; }` as the lighter 300 value made the orange on blue unreadable and `code { background-color: inherit; color: yellow; }` because the default orange on light gray was too jarring on the eyes. Otherwise, I quite like it.

Unfortunately there seems to be a snafu with rat's nest of dependencies used to build Bootswatch. When I ran `npm install` in the bootswatch folder after cloning <a href="https://github.com/thomaspark/bootswatch">the Bootswatch github repo</a>, I got an ugly error.

{% highlight bash %}
  npm ERR! Error: failed to fetch from registry: grunt-contrib-clean
  npm ERR!     at /usr/share/npm/lib/utils/npm-registry-client/get.js:139:12
{% endhighlight %}

I checked and `grunt-contrib-clean` is indeed found in the registry and I can fetch it from a browser. The debug log npm wrote doesn't provide any additional detail so I'm stuck. I'll try again in a few days and hope that somebody who knows how to fix it notices. Luckily the <a href="http://bootswatch.com/">Bootswatch site</a> offers ready to use minified CSS files for download and immediate use. 

