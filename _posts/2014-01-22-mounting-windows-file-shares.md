---
layout: post
title: "Mount a Windows file share in Ubuntu as a normal user"
tags: [ubuntu]
---

This is something I have figure out every time I come back to Ubuntu after not setting up a new machine for a long time.

First, the GUI for mounting Windows files shares never works for me. Not sure why, but I've never had luck with it.

So I resort to the command line. You can use fstab to do this, but my Windows shares only work when I'm on a VPN, which isn't all the time. So I want to be able to mount them on demand, only when needed. Also, fstab entries mount the share without the correct permissions to allow read/write by a non-root user.

My solution to this is gvfs-mount. This command adds a mounted "drive" to the Ubuntu file manager with working permissions.

    gvfs-mount smb://myserver.domain.com/myshare

It will prompt you for user name, password and domain. Haven't figured out how to script those yet. 

