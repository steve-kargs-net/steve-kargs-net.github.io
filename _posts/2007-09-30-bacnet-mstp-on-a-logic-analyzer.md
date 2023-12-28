---
id: 76
title: 'BACnet MS/TP on a Logic Analyzer'
date: '2007-09-30T18:56:18-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/bacnet-mstp-on-a-logic-analyzer/'
permalink: /bacnet/bacnet-mstp-on-a-logic-analyzer/
categories:
    - BACnet
---

I used to analyze BACnet MS/TP RS-485 traffic using an [HP54645D 100MHz 2+16 channel mixed signal oscilloscope](http://www.home.agilent.com/agilent/product.jspx?cc=US&lc=eng&ckey=1000001438:epsg:pro&nid=-536902796.536880488.00&id=1000001438:epsg:pro) because it had a deep buffer and MegaZoom which allowed me to see the data and timing of the frames. However, I have a new tool.

[![DigiView_MSTP.png](http://steve.kargs.net/wp-content/uploads/2007/thumbs/DigiView_MSTP.png "DigiView_MSTP.png")](http://steve.kargs.net/wp-content/uploads/2007/DigiView_MSTP.png)

Howard introduced me to [Digiview](http://www.tech-tools.com/dv_main.htm). The Digiview tool is a USB based logic analyzer. It permits you to view and decode signals. I set one of the signals to Async Decode, and gave the tool the baud rate, stop bits, parity of the signal. The software shows the logic signal and displays the decoded the data above the signal. The software also has time marker tools and allows you to set multiple time markers.

[![DigiView_MSTP_Timing.png](http://steve.kargs.net/wp-content/uploads/2007/thumbs/DigiView_MSTP_Timing.png "DigiView_MSTP_Timing.png")](http://steve.kargs.net/wp-content/uploads/2007/DigiView_MSTP_Timing.png)Using the DigiView tool and software, I am able to analyze BACnet MS/TP timing and frames with ease. I can see exactly how fast each node is responding and how long each node allows for the various BACnet MS/TP frames. I can also see exactly the content of each frame without having to decode the waveforms.

There are other mini logic analyzers on the market such as [BitScope](http://www.bitscope.com/), [USBee](http://www.usbee.com/), [PicoScope](http://www.picotech.com/), and the [Ant8 Logic Analyzer](http://www.usb-instruments.com/). [Jack Ganssle](http://www.ganssle.com/) wrote a [review](http://www.ganssle.com/microscopes.pdf) of some of them.