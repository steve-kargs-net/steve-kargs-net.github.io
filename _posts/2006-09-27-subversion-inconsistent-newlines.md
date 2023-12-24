---
id: 42
title: 'Subversion Inconsistent Newlines'
date: '2006-09-27T11:49:25-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/subversion-inconsistent-newlines/'
permalink: /bacnet/subversion-inconsistent-newlines/
categories:
    - applications
    - BACnet
---

[](http://steve.kargs.net/wp-content/uploads/2006/09/mstp-menu.jpg "SwitchPak MS/TP Menu")[![Copperhead snake at the Entrance to Bert Adams Scout Reservation](http://steve.kargs.net/wp-content/uploads/2006/09/copperhead.thumbnail.jpg "Copperhead snake at the Entrance to Bert Adams Scout Reservation")](http://steve.kargs.net/wp-content/uploads/2006/09/copperhead.jpg "Copperhead snake at the Entrance to Bert Adams Scout Reservation")I was minding my own business, coding the [BACnet stack project](http://bacnet.sourceforge.net/), and decided to commit some files to [subversion](http://subversion.tigris.org/) on [SourceForge](http://sourceforge.net/). However, [tortoise-svn](http://tortoisesvn.tigris.org/) gave me the “inconsistent newlines” error. I googled the problem, and found [a solution](http://svn.haxx.se/users/archive-2004-11/0857.shtml), but that solution didn’t fix the problem – it only masked the problem since my files were legitimate C files.

I fired up [SciTE ](http://www.scintilla.org/)with the problem file, and selected Options – Convert Line End Characters. After saving the changes, I promptly committed the problem file to subversion without having to change thesvn:eol-style option for that file. Problem solved!