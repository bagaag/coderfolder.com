---
date: 2014-01-23
layout: post
title:  "Customize Key Bindings in Ubuntu's Text Editor (GEdit)"
tags: [ubuntu]
---

I wanted to insert the date and time into a text file using a keystroke. Here's how.

1. Go to Edit menu -> Preferences -> Plugins tab
2. Enable the Insert Date/Time plugin
3. Click Preferences and select the format you like, otherwise it will prompt you every time.
4. Edit ~/.config/gedit/accels
5. Find this line:

 `    ; (gtk_accel_path "<Actions>/GeditTimePluginActions/InsertDateAndTime" "")`

 and replace it with this:

 `    (gtk_accel_path "<Actions>/GeditTimePluginActions/InsertDateAndTime" "F5")`

 Note that I removed the leading `;` and added F5 to the second quoted value. F5 is the key binding. Browse through the file to see how other key bindings are represented.

6. Save and restart GEdit.

