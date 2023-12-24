---
id: 75
title: 'Using GCC for ARM7 or AVR'
date: '2007-09-03T11:43:44-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/bacnet/using-gcc-for-arm7-or-avr/'
permalink: /bacnet/using-gcc-for-arm7-or-avr/
categories:
    - BACnet
    - Linux
    - software
---

Inspired by [Building Bare-Metal ARM Systems with GNU](http://www.embedded.com/design/opensource/200000632?_requestid=45088) series of articles, I recently ported the [BACnet MS/TP datalink layer](http://bacnet.sourceforge.net/) to an [Atmel AT91SAM7S-EK](http://www.atmel.com/dyn/products/other_docs.asp?family_id=605) board – an ARM7 processor – using a [GCC](http://gcc.gnu.org/) cross compiler for ARM.

I evaluated [GNU Toolchain for ARM](http://www.codesourcery.com/gnu_toolchains/arm), [GNU ARM](http://www.gnuarm.com/), [WinARM](http://www.siwawi.arubi.uni-kl.de/avr_projects/arm_projects/), and [YAGARTO](http://www.yagarto.de/) toolchains on the Windows platform. They all have their merits, but all have some slight differences too. I followed an excellent tutorial by James P. Lynch called *[Using Open Source Tools for AT91SAM7S Cross Development](http://www.atmel.com/dyn/resources/prod_documents/atmel_tutorial_source.zip)* to get me up and running quickly. Jim used the [YAGARTO](http://www.yagarto.de/) project as his toolchain.

I used the [YAGARTO](http://www.yagarto.de/) toolchain and created my own Makefile. Makefiles are an interesting bit of programming that seems to be a lost art. Any of the cross compiler toolchain builds should work with the Makefile with a slight modification to the name of the compiler (one of the differences in each of the various GNU ARM cross compiler projects).

During my travels down the [GCC](http://gcc.gnu.org/) road, I found the [GCC-AVR](http://www.avrfreaks.net/wiki/index.php/Documentation:AVR_GCC/AVR_GCC_Tool_Collection) and [WinAVR](http://winavr.sourceforge.net/) for Atmel AVR series of microcontrollers. I searched for GCC for an 8051. I found the [SDCC](http://sdcc.sourceforge.net/) project – Small Device C Compiler – for Intel 8051, Maxim 80DS390, Zilog Z80 and the Motorola 68HC08. Both projects are also in the [Ubuntu Linux](http://www.ubuntu.com/) repository. I noticed that the [Microchip](http://www.microchip.com/) [PIC24 compiler C30](http://www.microchip.com/stellent/idcplg?IdcService=SS_GET_PAGE&nodeId=1406&dDocName=en010065&part=SW006012) is based on GCC and the[ source code](http://www.microchip.com/stellent/idcplg?IdcService=SS_GET_PAGE&nodeId=1406&dDocName=en023073) is available on their website.