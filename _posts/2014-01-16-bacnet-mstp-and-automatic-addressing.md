---
id: 338
title: 'BACnet MS/TP and Automatic Addressing'
date: '2014-01-16T10:51:05-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=338'
permalink: /bacnet/bacnet-mstp-and-automatic-addressing/
categories:
    - BACnet
    - rights
---

[![Lego Coin Pusher Gamble](http://steve.kargs.net/wp-content/uploads/2014/01/IMAG3413-150x150.jpg)](http://steve.kargs.net/wp-content/uploads/2014/01/IMAG3413.jpg)A recent query on the [BACnet-L mailing list](http://www.bacnet.org/Contact/BACnet-L.htm) reminded me that I should probably post an update to my previous article about [BACnet and Software Patents](http://steve.kargs.net/bacnet/bacnet-and-software-patents/) in 2009. In the previous article, I lamented about a patent that was granted while the BACnet MS/TP working group had been working on standardizing several mechanisms to allow automatic MAC addressing.

The 3 methods of configuring an MS/TP MAC address without having to set a DIP switch that the MS/TP working group discussed many years ago included DHCP, ZeroConfig, and direct configuration via broadcast. Two of the methods have had proposals that moved from MS/TP working group into SSPC-135 BACnet committee in 2013, and are currently awaiting committee approval (or perhaps some updates from me).

[STK-030](http://steve.kargs.net/wp-content/uploads/2014/01/STK-030-15-MSTP-Zero-Config.doc): MSTP Zero-Config  
[STK-034](http://steve.kargs.net/wp-content/uploads/2014/01/STK-034-7.doc) (which combined [STK-028](http://steve.kargs.net/wp-content/uploads/2014/01/STK-028-8.doc)): Who-Am-I and You-Are services.  
[CG-005](http://steve.kargs.net/wp-content/uploads/2014/01/CG-005-1.doc): MSTP DHCP.

From STK-034:

> The Who-Am-I service is used by a sending BACnet-user to indicate that it requires identity configuration via the You-Are service.
> 
> The You-Are service is used by a client BACnet-user to configure the MAC address and BACnet Device object instance number in a remote device.

From the STK-030:

> This proposal describes a scheme for allowing devices to choose their own MAC address after monitoring the MS/TP line for available MAC addresses indicated by unanswered PollForMaster frames.
> 
> Since the token passes rapidly between nodes, and we must assume that the zero-configuration process may occur in the presence of statically configured nodes executing the current 135-2010 or earlier state machine, the only real opportunity to inject packet without holding a Token comes during the Poll For Master sequence.  
> \* Assume the node has listened to the token passing for a while and selected an address at random (or a previously used address) from the list of addresses that appear to be available. The addresses will be selected from a range of 64 to 127, leaving addresses 0 to 64 for fixed address nodes which will reduce the likelihood of collisions due to variable start up time.  
> \* Simply sending a Reply To Poll For Master is not enough of a confirmation, because there would be no way to distinguish nodes through their UIDs, nor to distinguish a dynamically addressed node from a statically configured node that happened to come online at that time.  
> \* After responding with a Reply To Poll For Master frame at an unused address, and receiving a Token frame, a Test Request frame will be sent by a node wishing to claim an address. The Test Request frame will include some unique information in the Data portion of the frame. This will cause the Poll For Master and Token sending node to reply with a Test Response frame which will include the unique data.  
> \* The zero configuration node will already have a list of peers, and can simply pass the Token to the Next Station, and continue with the normal Master Node State Machine.  
> \* The zero configuration node will monitor all MS/TP traffic, and will stop using its chosen MAC address if it sees another node communicating with an identical source MAC. The zero configuration node will start searching for another MAC at that time. The monitoring can be easily done after some modification to the DataNotForUs transition and SKIP\_DATA state of the Receive Node Finite State Machine for nodes that support Automatic Addressing of MS/TP.
> 
> This scheme was proposed during BACnet MS/TP working group meetings in Salt Lake City in June, 2008. The zero-configuration scheme was researched and developed, and actually implemented into products in May of 2010 to verify the approach, prior to creating this proposal in October of 2010.

There is an example of the STK-030 (initial proposed version – not up to date) method in the open source BACnet Protocol Stack hosted at [bacnet.sourceforge.net](http://bacnet.sourceforge.net/) in the [bacnet-stack/ports/stm32f10x/automac.c](http://svn.code.sf.net/p/bacnet/code/trunk/bacnet-stack/ports/stm32f10x/automac.c) and[ bacnet-stack/ports/stm32f10x/dlsmtp.c](http://svn.code.sf.net/p/bacnet/code/trunk/bacnet-stack/ports/stm32f10x/dlmstp.c) files. The STK-030 proposal was reviewed by KMC and does not infringe on their [patent](http://www.google.com/patents/about?id=wH_JAAAAEBAJ).