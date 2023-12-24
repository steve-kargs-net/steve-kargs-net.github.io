---
id: 51
title: 'BACnet Plugfest Complete'
date: '2006-10-06T00:37:39-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/bacnet-plugfest-complete/'
permalink: /bacnet/bacnet-plugfest-complete/
categories:
    - BACnet
    - software
---

Today was the final day of the [BACnet Interoperability Workshop](http://www.bacnetinternational.org/interop/), or Plugfest as it is commonly called. Over the two and a half days we found only two bugs in the [open source BACnet stack at SourceForge](http://bacnet.sourceforge.net/) that I [ported into our lighting panel in 5 days](http://steve.kargs.net/bacnet/bacnet-interoperability-workshop/). I fixed both bugs in a few minutes and uploaded the firmware into the lighting panels using the in-circuit-debugger. The fixes were verified by the other vendor.

![BTL Plugfest - Lighting panels and laptops](http://steve.kargs.net/wp-content/uploads/2006/10/plugfest-panels-small.jpg)

The MS/TP state machine worked. We tested it at 9600 baud, 19200 baud, and 38400 baud and worked fine. 76800 baud did not work, so I will need to figure out why. I may need to clock the processor at 40 MHz instead of 20 MHz to get some extra horsepower. I will also need to optimize the other processes, like the input reading and debouncing, to take less time in the main loop.

![Lithonia Lighting and Loytec testing BACnet and DALI and LON.](http://steve.kargs.net/wp-content/uploads/2006/10/lithonia-loytec.jpg)

The food was great and I met a lot of nice folks. Hopefully my flight home tomorrow will be uneventful.