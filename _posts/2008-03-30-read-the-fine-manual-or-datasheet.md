---
id: 85
title: 'Read the Fine Manual or Datasheet'
date: '2008-03-30T11:20:04-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/read-the-fine-manual-or-datasheet/'
permalink: /bacnet/read-the-fine-manual-or-datasheet/
categories:
    - BACnet
    - software
---

I found a bug in my [Atmel AVR](http://www.atmel.com/avr) ATmega168 port of the [BACnet Stack at SourceForge](http://bacnet.sourceforge.net/). It was the result of having not read the AVR datasheet close enough. Here is what the datasheet said:

> *The Transmit Complete (TXCn) Flag bit is set one when the entire frame in the Transmit Shift egister has been shifted out and there are no new data currently present in the transmit buffer. The TXCn Flag bit is automatically cleared when a transmit complete interrupt is executed, or it can be cleared by writing a one to its bit location.*

[![SAGE_Instruction_Counter.JPG](http://steve.kargs.net/wp-content/uploads/2008/.thumbs/.SAGE_Instruction_Counter.JPG "SAGE_Instruction_Counter.JPG")](http://steve.kargs.net/wp-content/uploads/2008/SAGE_Instruction_Counter.JPG)I had initially written the code to clear the TXC0 flag by clearing it, rather than setting it. Since the code could not determine when the end of the transmission occurred, I had added a \_delay\_us() function from the AVR-GCC library. This is what the AVR-GCC manual says about that function:

> *In order for these functions to work as intended, compiler optimizations must be enabled, and the delay time must be an expression that is a known constant at compile-time. If these requirements are not met, the resulting delay will be much longer (and basically unpredictable), and applications that otherwise do not use floating-point calculations will experience severe code bloat by the floating-point library routines linked into the application.*

[![ENIAC_tubes.jpg](http://steve.kargs.net/wp-content/uploads/2008/.thumbs/.ENIAC_tubes.jpg "ENIAC_tubes.jpg")](http://steve.kargs.net/wp-content/uploads/2008/ENIAC_tubes.jpg)Severe code bloat indeed! I had used a non-constant (the Baud Rate) in the delay call, and that resulted in a 4k increase in code size. After fixing the Transmit Complete flag functionality, I was able to remove the \_delay\_us, and the code size dimimished by 4k. On this 16k device, that means alot!

Statistics for the BACnet Stack at SourceForge on the ATmega168 are as follows:

IAR Atmel AVR C/C++ Compiler V5.10A/W32  
10 191 bytes of CODE memory (+ 36 range fill )  
775 bytes of DATA memory (+ 24 absolute )

avr-gcc (GCC) 4.2.2 (WinAVR 20071221rc1)  
Program: 12052 bytes (73.6% Full)  
Data: 481 bytes (47.0% Full)

With all the extra code space, I went on to add more functionality to the demo. The [BACnet](http://www.bacnet.org/) capabilities include WhoIs, I-Am, ReadProperty, and WriteProperty support. The BACnet objects include a Device object, 10 Binary Value objects, and 10 Analog Value objects. An LED is controlled by Binary Value object instance 0. All required object properties can be retrieved using ReadProperty. The Present\_Value property of the Analog Value and Binary Value objects can be written using WriteProperty. The Object\_Identifier, Object\_Name, Max\_Info\_Frames, Max\_Master, and baud rate (property 9600) of the Device object can be written using WriteProperty.

After adding all that functionality, I learned the hard way about the C-Stack differences between the IAR AVR compiler and the GCC-AVR compiler. The IAR compiler uses a fixed CStack size. If it is not set correctly, the CStack can overflow and cause problems in your code.

[![Johnniac.jpg](http://steve.kargs.net/wp-content/uploads/2008/.thumbs/.Johnniac.jpg "Johnniac.jpg")](http://steve.kargs.net/wp-content/uploads/2008/Johnniac.jpg)The GCC compiler uses the [RAM not allocated to variables and text for the C-Stack](http://www.cs.utah.edu/~regehr/stacktool/). That means that the data value reported by the avr-size program is only part of the picture. If the data value is 481 bytes, and the device has 1024 total, then 1024-481=543 bytes are used by the C-Stack. In other words, don’t be fooled by the “47% Full” printed by avr-size and think that you have extra RAM. You might be able to add some more functionality, but certainly leave some RAM (or alot in my case) for the C-Stack. The GCC-AVR has two intrinsic variables for tracking the C-Stack: \_end and \_\_stack. These can be used to [paint the C-Stack prior to its usage, and monitor the C-Stack during runtime](http://www.avrfreaks.net/index.php?name=PNphpBB2&file=printview&t=52249&start=0). I added this technique to the demo.

The final statistics on ATmega168 demo of the [BACnet Stack at SourceForge](http://bacnet.sourceforge.net/):

IAR Atmel AVR C/C++ Compiler V5.10A/W32  
12 732 bytes of CODE memory (+ 36 range fill )  
955 bytes of DATA memory (+ 24 absolute ) (CStack=0x200)

avr-gcc (GCC) 4.2.2 (WinAVR 20071221rc1)  
Program: 15790 bytes (96.4% Full)  
Data: 414 bytes (40.4% Full) (CStack=0x262)

Note: The photos are ancient computer memory from [The Computer History Museum](http://www.computerhistory.org/) in [Mountain View, California](http://en.wikipedia.org/wiki/Mountain_View%2C_California). I’m visiting the area for the [Wireshark Sharkfest ’08](http://www.cacetech.com/SHARKFEST.08/).