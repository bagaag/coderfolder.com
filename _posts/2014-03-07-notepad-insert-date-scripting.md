---
layout: post
title:  "Custom Date Insert Plugin for Notepad++"
tags: editors
---

I've been using <a href="http://notepad-plus-plus.org/">Notepad++</a> on my Windows machine at work. It's the best free editor for Windows that I'm aware of, and does pretty much everything I can think of, with one notable exception. 

Any editor that calls itself a programmer's editor should be scriptable. While you can develop your own plugins for Notepad++, it's not at all a trivial affair. Something like inserting the current date and time in a specific format is a trivial task, and shouldn't require a compiled C++ project made up of a dozen files. 

Luckily, <a href="https://github.com/davegb3">someone handy with C++</a> realized the same thing, and developed a plugin to allow <a href="http://npppythonscript.sourceforge.net/">Python scripting of Notepad++</a>. 

My specific need was to frequently insert the current date and time into the editor with the format YYYY-MM-DD HH-mm. The kitchen-sink TextFX plugin provides an Insert Date function, but only supports the standard "short" and "long" formats specified in your Windows system preferences. 

Here's how I got it working.

<ol>
<li>Install the NPPPythonScript plugin. See the <a href="http://npppythonscript.sourceforge.net/docs/latest/usage.html">excellent documentation</a> for assistance if you don't know how to install plugins.</li>

<li>Create the following ridiculously trivial Python script using the plugin:</li>

{% highlight python %}
import datetime
now = datetime.datetime.now()
editor.addText(now.strftime("%Y-%m-%d %H:%M "))
{% endhighlight %}

This allows you to run it from the Python Script plugin's menu. But I need to run this script a lot, so a keyboard shortcut is... key.

<li>Use the Python Script plugin's Configuration dialog to add a menu item for my new script.</li>

<li>Use Notepad++'s Shortcut Mapper to map a keyboard shortcut to my script. Its found in the Plugins section of the Shortcut Mapper.</li>
</ol>

... and voila.

The scripts are created/saved in the `C:\Users\[user name]\AppData\Roaming\Notepad+\plugins\config\PythonScript\scripts` folder.


