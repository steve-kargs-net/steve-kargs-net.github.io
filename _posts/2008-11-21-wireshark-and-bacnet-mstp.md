---
id: 139
title: 'Wireshark and BACnet MS/TP'
date: '2008-11-21T01:26:51-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=139'
permalink: /bacnet/wireshark-and-bacnet-mstp/
categories:
    - BACnet
---

[![](http://steve.kargs.net/wp-content/uploads/2008/11/wireshark_bacnet_mstp_cimetrics-150x150.png "wireshark_bacnet_mstp_cimetrics")](http://steve.kargs.net/wp-content/uploads/2008/11/wireshark_bacnet_mstp_cimetrics.png)

I wrote an article about [Analyzing BACnet with Wireshark](http://www.bacnet.org/Bibliography/BACnet-Today-08/Karg_2008.pdf) for [ASHRAE Journal](http://www.ashrae.org/publications/page/540) special supplement BACnet Today. [ASHRAE](http://www.ashrae.org/) is very particular about endorsing specific company products, and removed some references I had to information about how BACnet MS/TP can be supported on Wireshark by adding an external interface which sends Ethernet SNAP protocol packets. The external interface was originally a [Cimetrics U+4](http://cimetrics.com/products/proddetail.php?prod=B2110&cat=1) device which connects BACnet MS/TP via USB to a computer, and uses a special driver to appear as a network interface to [Wireshark](http://wireshark.org/).

In April, 2008, I was informed that the Cimetrics U+4 packets showed up in Wireshark, but were not decoded correctly. I asked for a sample of the capture, and reverse engineered the header. I then created the BACnet MS/TP decoding in Wireshark in order to display the MS/TP data, and passed the BACnet Network Layer and Application Layer information along to the existing dissectors.

The beauty of the BACnet protocol is that it is layered. The NPDU (network layer) and APDU (application layer) encodings are the same regardless of the datalink layer used. The NDPU layer is decoded by [packet-bacnet.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-bacnet.c), which passes the APDU layer to [packet-bacapp.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-bacapp.c). The BACnet MS/TP datalink layer is decoded by [packet-mstp.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-mstp.c) which I created, and passes the NPDU, if it exists, to [packet-bacnet.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-bacnet.c), for decoding. The ARCNET, Ethernet, and BACnet/IP ([packet-bvlc.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-bvlc.c)) all pass a relevant packet to [packet-bacnet.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-bacnet.c) for BACnet decoding. I created [packet-cimetrics.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-cimetrics.c) for the Cimetrics header which passes the BACnet MS/TP datalink layer to [packet-mstp.c](http://anonsvn.wireshark.org/wireshark/trunk/epan/dissectors/packet-mstp.c).

The BACnet MS/TP patches were accepted into the [Wireshark ](http://wireshark.org/)repository on May 13, 2008, checked in as SVN 25291. The SVN 25881 was a fix to the Length decoding. The BACnet MS/TP decoding eventually made it into the [Wireshark 1.1 development release](http://www.wireshark.org/download/), but is not present in the Wireshark 1.0 stable release.

Wireshark now sees packets with the Cimetrics U+4 signature encapsulated in the SNAP protocol as MS/TP packets, and it is able to open a file that has been saved in PCAP format using the MS/TP WTAP signature. But I didn’t have a Cimetrics U+4 device. So I used a standard RS485 converter, my [open source BACnet stack](http://bacnet.sourceforge.net/), and wrote [a simple application to packetize the MS/TP frames](http://bacnet.svn.sourceforge.net/viewvc/bacnet/trunk/bacnet-stack/demo/mstpcap/) and saves them to PCAP format. I could now capture MS/TP packets and view them!

In August, 2008, I received an email from John in New Zealand. His intention was “to use an existing simple VB application that captures MS/TP traffic from a low cost USB to RS-485 converter, to send the MS/TP packets using Winsock/UDP to Wireshark for final dissection and display.” I figured that we could do this by making use of the existing [SNAP protocol](http://en.wikipedia.org/wiki/Subnetwork_Access_Protocol) dissector that I created for the Cimetrics packets.

I reused the code that I had written to save in PCAP format, and wrote [a simple application](http://bacnet.svn.sourceforge.net/viewvc/bacnet/trunk/bacnet-stack/ports/linux/mstpsnap.c) to packetize the MS/TP frames and resend them on Ethernet as the Cimetrics U+4 signature encapsulated in the SNAP protocol. I got it to work under Linux, but would probably need to use WinPcap to get it to work under Windows.

Sending those [SNAP protocol](http://en.wikipedia.org/wiki/Subnetwork_Access_Protocol) packets on Ethernet allows the display of BACnet MS/TP packets in realtime alongside BACnet/IP and BACnet Ethernet. This makes it very easy to relate traffic going to and from workstations and routers with what is happening on the BACnet MS/TP network.

There are some [sample captures](http://kargs.net/captures/) (see [cimetrics\_mstp.pcap](http://kargs.net/captures/cimetrics_mstp.pcap) and [mstp\_wtap.cap](http://kargs.net/captures/mstp_wtap.cap)) that demostrate some of the abilities of Wireshark.[  ](http://kargs.net/captures/)

I use a USB to RS-485 converter from SerialGear [USB-COMi-SI-M](http://www.serialgear.com/Industrial-Serial-Adapters-USB-COMi-SI-M.html), and am told that the [B&amp;B Electronics USOPTL4](http://www.bb-elec.com/bb-elec/literature/USxPTL4-1207ds.pdf) works very well. I am also told that the USB to RS-485 adapters that use the FTDI chipset are great for this as they allow the use of 76800 baud which is usually the stumbling block for native MS/TP interfacing with a standard PC serial port.