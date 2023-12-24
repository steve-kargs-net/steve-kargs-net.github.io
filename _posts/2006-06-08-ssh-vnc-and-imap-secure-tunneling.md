---
id: 14
title: 'ssh, VNC, and IMAP secure tunneling'
date: '2006-06-08T11:59:05-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/applications/ssh-vnc-and-imap-secure-tunneling/'
permalink: /applications/ssh-vnc-and-imap-secure-tunneling/
categories:
    - applications
    - Linux
---

I run an IMAP server in the garage so that I can have my e-mail and folders in a central location. I have a domain name that I point to [zoneedit.com](http://zoneedit.com/) and use [ddclient](http://ddclient.sourceforge.net/) to update the IP address. From Windows, I access the IMAP using an ssh tunnel with the fine [PuTTY ssh client](http://www.chiark.greenend.org.uk/~sgtatham/putty/). From Linux, I just use the command line. I setup a local ssh IMAP tunnel to the potter machine which sets up the tunnel via the localhost:  
`$ sudo ssh -L143:potter:143 karg.us`

I can then read email using [Mozilla Thunderbird](http://www.mozilla.org/) by configuring IMAP to use localhost on the standard port (143).

![Happy Jet](http://steve.kargs.net/wp-content/uploads/2006/06/jet_happy.jpg "Happy Jet")

ssh tunneling is also handy for troubleshooting. To do remote troubleshooting, a remote desktop control tool is need, and I use [Tight VNC](http://www.tightvnc.com/). To launch a [Tight VNC](http://www.tightvnc.com/) session to help my wife restart the printer queue, I run:  
`$ ssh -L5901:wilbur:5900 karg.us`  
`$ xtightvncviewer -encodings "tight copyrect" localhost:1`

Simple, right?