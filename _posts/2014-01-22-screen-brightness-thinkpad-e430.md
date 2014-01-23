---
layout: post
title: Get the screen brightness keys working in Ubuntu on the Thinkpad E430
categories: ubuntu
---

The hardware on the Thinkpad E430 has thus far worked perfectly in Ubuntu with one exception. The screen brightness function keys. This post on askubuntu explains the problem and solution.

[http://askubuntu.com/questions/293925/brightness-buttons-not-working-properly](http://askubuntu.com/questions/293925/brightness-buttons-not-working-properly)

The fix:

1. `sudo vim /etc/default/grub`
2. Look for the line that says `GRUB_CMDLINE_LINUX=""` and change it to this: `GRUB_CMDLINE_LINUX="acpi_osi=\"!Windows 2012\""`
3. `sudo update-grub`
4. Reboot
