---
id: 154
title: 'AVR ISP mkII on Ubuntu Hardy'
date: '2009-05-12T20:10:52-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=154'
permalink: /bacnet/avr-isp-mkii-on-ubuntu-hardy/
categories:
    - BACnet
    - Linux
    - software
---

[![BACnet Development Kit](http://steve.kargs.net/wp-content/uploads/2009/05/bdk-atxx4-mstp-150x150.jpg "bdk-atxx4-mstp")](http://steve.kargs.net/wp-content/uploads/2009/05/bdk-atxx4-mstp.jpg)

I created a [BACnet Development Kit](http://bacnetdevelopmentkit.com/), compiled the [open source BACnet Protocol Stack hosted on SourceForge.net](http://bacnet.sourceforge.net/) firmware using [gcc-avr](http://www.avrfreaks.net/AVRGCC/), and attempted to load the firmware onto the kit using an [Atmel AVR ISP mkII](http://www.atmel.com/dyn/Products/tools_card.asp?tool_id=3808) USB programmer. I connected the AVR ISP mkII to my Ubuntu Hardy Linux PC and attached the 2×3 ISP cable to the development kit board, and attempted to program using [avrdude](http://www.bsdhome.com/avrdude/):

```
$ avrdude -c avrispmkII -p m644p -P usb -e -U flash:w:bacnet.hex
```

```
avrdude: usb_open(): cannot read serial number "error sending..."
avrdude: usb_open(): cannot read product name "error sending..."
avrdude: usbdev_open(): error setting configuration...
avrdude: usbdev_open(): did not find any USB device "usb"
```

Wow! That wasn’t nice. A search on the Internet turned up [some answers about how to fix the problem](http://www.avrfreaks.net/index.php?name=PNphpBB2&t=58673&start=0), and I modified my /etc/udev/avarice.rules file to look like this:

```
SUBSYSTEM!="usb_device", ACTION!="add", GOTO="avarice_end"

# Atmel Corp. JTAG ICE mkII
SYSFS{idVendor}=="03eb", SYSFS{idProduct}=="2103", MODE="660", GROUP="dialout"
# Atmel Corp. AVRISP mkII
SYSFS{idVendor}=="03eb", SYSFS{idProduct}=="2104", MODE="660", GROUP="dialout"
# Atmel Corp. Dragon
SYSFS{idVendor}=="03eb", SYSFS{idProduct}=="2107", MODE="660", GROUP="dialout"

LABEL="avarice_end"
```

I disconnected and reconnected my AVR ISP mkII, and tried again. I still had the same results. I checked that I was a member of the dialout group:

```
$ groups
skarg adm dialout cdrom floppy audio dip video plugdev users fuse lpadmin admin
```

I looked at the symbolic link in the /etc/udev/rules.d/ directory and also consumed the README file. My file had the following name:

```
/etc/udev/rules.d/z60_avarice.rules
```

So I changed the filename:

```
$ sudo mv /etc/udev/rules.d/z60_avarice.rules /etc/udev/rules.d/60-avarice.rules
```

I unplugged the AVR ISP mkII, and plugged it in again. I tried to run avrdude again:

```
avrdude -c avrispmkII   \
     -p m644p -P usb -e        \
     -U flash:w:bacnet.hex

avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.01s

avrdude: Device signature = 0x1e960a
avrdude: erasing chip
avrdude: reading input file "bacnet.hex"
avrdude: input file bacnet.hex auto detected as Intel Hex
avrdude: writing flash (57406 bytes):

Writing | ################################################## | 100% 6.31s

avrdude: 57406 bytes of flash written
avrdude: verifying flash memory against bacnet.hex:
avrdude: load data flash data from input file bacnet.hex:
avrdude: input file bacnet.hex auto detected as Intel Hex
avrdude: input file bacnet.hex contains 57406 bytes
avrdude: reading on-chip flash data:

Reading | ################################################## | 100% 5.41s

avrdude: verifying ...
avrdude: 57406 bytes of flash verified

avrdude: safemode: Fuses OK

avrdude done.  Thank you.
```

The kit programmed successfully, and began operation.