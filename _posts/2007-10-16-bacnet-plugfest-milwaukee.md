---
id: 77
title: 'BACnet Plugfest &#8211; Milwaukee'
date: '2007-10-16T23:29:41-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/bacnet-plugfest-milwaukee/'
permalink: /bacnet/bacnet-plugfest-milwaukee/
categories:
    - BACnet
---

[![ATmega168 running BACnet](http://steve.kargs.net/wp-content/uploads/2007/thumbs/ATmega168_BACnet.jpg "ATmega168 running BACnet")](http://steve.kargs.net/wp-content/uploads/2007/ATmega168_BACnet.jpg)I attended the [BACnet Interoperability Workshop](http://bacnetinternational.org/) again this year. The Plugfest was held in Milwaukee. I tested another [BACnet Stack at SourceForge](http://bacnet.sourceforge.net/) enabled device. This time it was an Atmel AVR ATmega168 using the [GCC WinAVR](http://winavr.sourceforge.net/) compiler. It was utilizing the [BACnet](http://www.bacnet.org/) MS/TP datalink layer, and had a Device object and 9 Analog Input objects inside. It supported the ReadProperty service, and WhoIs and I-Am services for binding. It had a Maximum APDU size of 128 bytes.  
AVR Memory Usage  
—————-  
Device: atmega168

Program: 16350 bytes (99.8% Full)  
(.text + .data + .bootloader)

Data: 630 bytes (61.5% Full)  
(.data + .bss + .noinit)

Here is the key that helped me fit the code. I found a [GCC compiler and linker directive](http://gcc.gnu.org/ml/gcc-help/2003-08/msg00128.html) that allowed all the unused functions and dead code to be removed. I found the directive initially on the [GCC M68HC11 FAQ](http://m68hc11.serveftp.org/wiki/index.php/FAQ:Link#How_can_I_remove_unused_functions.3F). It saved me from having to split out all the functions into separate files and put them into a single library.

[![Wireshark_NPDU.png](http://steve.kargs.net/wp-content/uploads/2007/thumbs/Wireshark_NPDU.png "Wireshark_NPDU.png")](http://steve.kargs.net/wp-content/uploads/2007/Wireshark_NPDU.png)I also met some great folks, some of whom were using the [BACnet Stack at SourceForge](http://bacnet.sourceforge.net/) in their products. I also saw a lot of folks using [Wireshark](http://wireshark.org/) for BACnet protocol analysis. I also got to see a lot of friends that I have made over the years.

Edit: I compiled the project with [IAR AVR version 4 compiler](http://www.iar.com/) and here are the memory usage statistics:

IAR AVR:  
10 055 bytes of CODE memory (+ 36 range fill )  
553 bytes of DATA memory (+ 24 absolute )