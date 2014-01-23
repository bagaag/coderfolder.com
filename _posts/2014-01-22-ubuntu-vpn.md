---
layout: post
title:  "Ubuntu VPN Troubleshooting"
categories: ubuntu
---

Trying to get a VPN to a Windows 2008 server working on a fresh Ubuntu 12.04 install. Just gave me a useless "connection failed" message. Here's what fixed it:

* Logged into the connection on a Windows machine, looked at the connection properties and noted the Authenticaion and Encryption settings. 
* Found the Authentication and Encryptiong settings on the Ubuntu connection in Advanced settings.

In short, Ubuntu wasn't guessing these settings correctly for some reason and needed to be told.

