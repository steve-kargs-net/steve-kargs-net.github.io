---
id: 389
title: 'BACnet MS/TP Wireshark Live Capture'
date: '2016-09-16T17:27:39-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=389'
permalink: /bacnet/bacnet-mstp-wireshark-live-capture/
categories:
    - BACnet
---

[Wireshark](https://www.wireshark.org/) 2.0 brought some new features, including [extcap](https://www.wireshark.org/docs/man-pages/extcap.html). Extcap allows an external application to capture packets and move them into Wireshark via a pipe. It is the perfect feature for serial packets, such as BACnet MS/TP on RS-485, which don’t have a network interface.

How does it work? After installing version Wireshark 2.0 or later, find the Extcap folder on your computer. The folder is listed under Wireshark Help About Folders menu option.

[![help-about-wireshark-folders](http://steve.kargs.net/wp-content/uploads/2016/09/Help-About-Wireshark-Folders-300x141.png)](http://steve.kargs.net/wp-content/uploads/2016/09/Help-About-Wireshark-Folders.png)

Copy [mstpcap.exe](https://sourceforge.net/projects/bacnet/files/bacnet-tools/) into the Extcap folder (create the folder if it doesn’t exist).

[![program-files_wireshark_extcap](http://steve.kargs.net/wp-content/uploads/2016/09/Program-Files_Wireshark_extcap-300x131.png)](http://steve.kargs.net/wp-content/uploads/2016/09/Program-Files_Wireshark_extcap.png)

Run Wireshark, and notice the new BACnet MS/TP Interfaces associated with each serial port.

[![wireshark-interface-list](http://steve.kargs.net/wp-content/uploads/2016/09/Wireshark-Interface-List-229x300.png)](http://steve.kargs.net/wp-content/uploads/2016/09/Wireshark-Interface-List.png)

Adjust the MS/TP Baud Rate for the particular interface.

[![wireshark-mstp-interface-settings](http://steve.kargs.net/wp-content/uploads/2016/09/Wireshark-MSTP-Interface-Settings-300x199.png)](http://steve.kargs.net/wp-content/uploads/2016/09/Wireshark-MSTP-Interface-Settings.png)

Start or Stop captures using the Capture Start or Capture Stop options after selecting the Interface.

[![bacnet_ms_tp_on_com6_wireshark_start_capture](http://steve.kargs.net/wp-content/uploads/2016/09/BACnet_MS_TP_on_COM6_Wireshark_Start_Capture-300x97.png)](http://steve.kargs.net/wp-content/uploads/2016/09/BACnet_MS_TP_on_COM6_Wireshark_Start_Capture.png)