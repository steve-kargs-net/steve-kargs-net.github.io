---
id: 374
title: 'Raspberry PiFace'
date: '2015-03-19T12:10:24-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=374'
permalink: /bacnet/raspberry-piface/
categories:
    - BACnet
    - Linux
---

[![](http://steve.kargs.net/wp-content/uploads/2015/03/IMG_20140604_081350813-150x150.jpg)](http://steve.kargs.net/wp-content/uploads/2015/03/IMG_20140604_081350813.jpg)

I have been using a [Raspberry Pi](http://www.raspberrypi.org/) for various things since it was invented. It is a great little low cost computer. We recently celebrated Pi Day (3/14/15) here in the USA. Our local [Science Center](http://www.mcwane.org/) hosted a Pi Day programming workshop using Raspberry Pi, and my teenage daughter attended with her cousin and a friend. The following day, Anna showed me on her [Ubuntu](http://www.ubuntu.com/) laptop how to use [Scratch](https://scratch.mit.edu/) to perform some programming, and also showed me the [Squirrel Eat Squirrel](http://inventwithpython.com/pygame/chapter8.html) game in Python that she modified.

At the [BACnet](http://www.bacnet.org/) Summer 2014 meeting, I was given a Raspberry Pi and a PiFace card when I was presented the BACnet Swan Award. During that meeting, I decided it would be fun to play with the Raspberry Pi and the PiFace card. I first made a [Raspian](http://www.raspbian.org/) SD card, connected an Ethernet cable from my laptop, connected to the Raspberry Pi via SSH, downloaded the PiFace interface code, installed the build tools (apt-get build-essentials) and [BACnet Protocol Stack](http://bacnet.sourceforge.net/), and wrote a quick BACnet example application that modeled the inputs as Binary Inputs and relays as Binary Outputs using the open source [BACnet Protocol Stack](http://bacnet.sourceforge.net/) library hosted on [Sourceforge.net](http://sourceforge.net/). I posted the project in the [demo/](http://svn.code.sf.net/p/bacnet/code/trunk/bacnet-stack/demo/piface/) folder of the project during the meeting. My friend [David Fisher](https://www.linkedin.com/profile/view?id=12059891), who originated the BACnet Swan Award in memory of our friend [Bill Swan](http://www.bacnet.org/DL-Docs/Swan-in-Memoriam.html), kindly tested the BACnet interface to verify interoperability (and make some relays click!) over the WiFi LAN we configured for the meeting.