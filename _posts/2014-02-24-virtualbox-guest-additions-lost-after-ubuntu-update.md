---
layout: default
title: Virtualbox guest additions lost after updating Ubuntu
tags: ubuntu virtualbox 
---

If you are running Ubuntu as a Virtualbox guest, the automagic screen resolution, mouse scrolling and other guest addition goodies may stop working after running apt-get upgrade. This is because the guest additions get lost when an updated kernel is installed. Here's the fix:

`sudo apt-get install virtualbox-guest-dkms`

Then restart the Ubuntu guest.

