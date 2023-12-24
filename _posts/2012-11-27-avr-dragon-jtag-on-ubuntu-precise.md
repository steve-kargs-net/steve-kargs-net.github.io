---
id: 325
title: 'AVR Dragon JTAG on Ubuntu Precise'
date: '2012-11-27T23:16:42-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=325'
permalink: /linux/avr-dragon-jtag-on-ubuntu-precise/
categories:
    - Linux
---

[![Lt. Col. Pat Ichi Karg at Little Rock Air Show in F4 Phantom](http://steve.kargs.net/wp-content/uploads/2012/11/f4-pass-2-150x150.jpg "f4-pass-2")](http://steve.kargs.net/wp-content/uploads/2012/11/f4-pass-2.jpg)I have a [BACnet Development Kit](http://bacnetdevelopmentkit.com/) which uses the example firmware compiled from the [open source BACnet Protocol Stack hosted on SourceForge.net](http://bacnet.sourceforge.net/) using [gcc-avr](http://www.avrfreaks.net/AVRGCC/). I attempted to load the firmware onto the kit using an [Atmel AVR Dragon](http://www.atmel.com/tools/avrdragon.aspx) USB JTAG programmer. I connected the AVR Dragon to my Ubuntu Precise Linux Laptop and attached the 2×5 JTAG cable to the development kit board, and attempted to program using [avrdude](http://www.bsdhome.com/avrdude/) as I had many times over the last several years.

```
avrdude -c dragon_jtag -p m644p -P usb -B 8 -U hfuse:w:0x93:m -U lfuse:w:0xD7:m -U efuse:w:0xFC:m
```

```
avrdude: usb_open(): cannot read serial number "error sending control message: Operation not permitted"
avrdude: usb_open(): cannot read product name "error sending control message: Operation not permitted"
avrdude: usbdev_open(): error setting configuration 1: could not set config 1: Operation not permitted
avrdude: usbdev_open(): did not find any USB device "usb"
make: *** [writefuses] Error 1
```

Aha, I said, I must need to [edit the UDEV rules for AVRICE](http://steve.kargs.net/bacnet/avr-isp-mkii-on-ubuntu-hardy/)as I did previously. But alas, that did not solve the problem. It seems the syntax for the UDEV rules have changed from using ‘SYSFS’ to using ‘ATTR’, and so the new rules use the following text in a /etc/udev/rules.d/45-atmel.rules file :

```
# udev rules file for atmel usb devices (for udev 0.98 version) 
# 
SUBSYSTEM!="usb_device", ACTION!="add", GOTO="avrisp_end"
```

```
# Atmel Corp.JTAG ICE mkII 
ATTR{idVendor}=="03eb", ATTR{idProduct}=="2103", MODE="660", GROUP="dialout"
```

```
# Atmel Corp. AVRISP mkII
ATTR{idVendor}=="03eb", ATTR{idProduct}=="2104", MODE="660", GROUP="dialout"
```

```
# Atmel Corp. Dragon
ATTR{idVendor}=="03eb", ATTR{idProduct}=="2107", MODE="660", GROUP="dialout"
```

```
LABEL="avrisp_end"
```

After saving the file, unplugging and plugging the AVR Dragon into the USB port, I was finally able to program the board.

```
avrdude -c dragon_jtag -p m644p -P usb -B 8 -U hfuse:w:0x93:m -U lfuse:w:0xD7:m -U efuse:w:0xFC:m
```

```
avrdude: jtagmkII_initialize(): warning: OCDEN fuse not programmed, single-byte EEPROM updates not possible
avrdude: AVR device initialized and ready to accept instructions
```

```
Reading | ################################################## | 100% 0.00s
```

```
avrdude: Device signature = 0x1e960a
avrdude: reading input file "0x93"
avrdude: writing hfuse (1 bytes):
```

```
Writing | ################################################## | 100% 0.01s
```

```
avrdude: 1 bytes of hfuse written
avrdude: verifying hfuse memory against 0x93:
avrdude: load data hfuse data from input file 0x93:
avrdude: input file 0x93 contains 1 bytes
avrdude: reading on-chip hfuse data:
```

```
Reading | ################################################## | 100% 0.00s
```

```
avrdude: verifying ...
avrdude: 1 bytes of hfuse verified
avrdude: reading input file "0xD7"
avrdude: writing lfuse (1 bytes):
```

```
Writing | ################################################## | 100% 0.01s
```

```
avrdude: 1 bytes of lfuse written
avrdude: verifying lfuse memory against 0xD7:
avrdude: load data lfuse data from input file 0xD7:
avrdude: input file 0xD7 contains 1 bytes
avrdude: reading on-chip lfuse data:
```

```
Reading | ################################################## | 100% 0.00s
```

```
avrdude: verifying ...
avrdude: 1 bytes of lfuse verified
avrdude: reading input file "0xFC"
avrdude: writing efuse (1 bytes):
```

```
Writing | ################################################## | 100% 0.01s
```

```
avrdude: 1 bytes of efuse written
avrdude: verifying efuse memory against 0xFC:
avrdude: load data efuse data from input file 0xFC:
avrdude: input file 0xFC contains 1 bytes
avrdude: reading on-chip efuse data:
```

```
Reading | ################################################## | 100% 0.00s
```

```
avrdude: verifying ...
avrdude: 1 bytes of efuse verified
```

```
avrdude: safemode: Fuses OK
```

```
avrdude done. Thank you.
```