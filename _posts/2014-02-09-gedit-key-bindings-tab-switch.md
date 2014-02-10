---
layout: post
title: "Changing the key mapping for switching tabs in gedit"
tags: ubuntu
---

The default text editor in Ubuntu is gedit. If you're coming from Windows, you probably think this is akin to Notepad and should be immediately discarded as an option for use beyond the simplest of editing tasks. 

It turns out gedit is pretty powerful. Not only does it do all the standard stuff a relatively robust editor can do, it is programmatically extensible - the most important feature of a text editor. 

One of the common peeves about gedit, however, is the silly default key mapping for tab switching. Ctrl-Alt-PageUp and Ctrl-Alt-PageDown are stupid choices for something performed so often when editing multiple files. 

There's hope. You can change these by editing the .config/gedit/accels file in your user folder. Look for these lines (note, they are not next to eachother):

    ; (gtk_accel_path "<Actions>/GeditWindowActions/DocumentsPreviousDocument" 
      "<Primary><Alt>Page_Up")
    ; (gtk_accel_path "<Actions>/GeditWindowActions/DocumentsNextDocument" 
      "<Primary><Alt>Page_Down")

Change the second quoted parameter to indicate the new key mapping. Peruse through the file to get a sense of your options and how to specify certain key mappings. Also, remove the `; ` at the begining. This activates the directive to override the default. I chose Ctrl-T and Ctrl-Shift-T:

    (gtk_accel_path "<Actions>/GeditWindowActions/DocumentsPreviousDocument" 
      "<Primary><Shift>t")
    (gtk_accel_path "<Actions>/GeditWindowActions/DocumentsNextDocument" "<Primary>t")

Note that `<Primary>` here is the Ctrl key, at least on my keyboard.

I tried to use `<Primary>Page_Up` and `<Primary>Page_Down` as these seem to be standard on most tabbed editors, but I wasn't able to get them to work. If you did, drop a comment and let me know how.

