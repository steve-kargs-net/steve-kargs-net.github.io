---
id: 212
title: 'Wireshark on Ubuntu not as root'
date: '2010-10-21T16:03:28-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=212'
permalink: /bacnet/wireshark-on-ubuntu-not-as-root/
categories:
    - BACnet
    - Linux
tags:
    - bacnet
    - wireshark
---

[![](http://steve.kargs.net/wp-content/uploads/2010/10/chris-mario-happy-176x300.jpg "chris-mario-happy")](http://steve.kargs.net/wp-content/uploads/2010/10/chris-mario-happy.jpg)I often need to capture [BACnet](http://www.bacnet.org/) network traffic using [Wireshark](http://wireshark.org/) while I am running [Ubuntu Linux](http://ubuntu.com/). I’ve always had to run Wireshark as root (usually via gksu or kdesu) in order to capture from any interfaces (i.e. eth0, wlan0). For awhile, there was an additional Wireshark menu item that included the “run as root” option. However, running an application “as root” has some downsides (like being insecure), and in the latest release of Ubuntu, there is no menu item to run “as root”. The downside of running as root for me was that the capture files saved by default into /root directory, and saved with root group and owner permissions.

Today, after launching the menu and seeing no interfaces (again), I decided to search the Internet and find a better way, and found two things of note. The first method, which I found posted on [Ubuntu Forums](http://start.ubuntuforums.org/showthread.php?p=9903794#post9903794), is the manual way of configuring Wireshark to run as a normal user (with admin group privileges) by configuring only dumpcap to have the elevated privileges:

```
$ sudo apt-get install libcap2-bin wireshark
$ sudo chgrp admin /usr/bin/dumpcap
$ sudo chmod 750 /usr/bin/dumpcap
$ sudo setcap cap_net_raw,cap_net_admin+eip /usr/bin/dumpcap
```

The second method was outlined in [Ubuntu Bug #513903 at Lauchpad](https://bugs.launchpad.net/ubuntu/+source/wireshark/+bug/513903) and can be done with Ubuntu Lucid and beyond. It creates a new group “wireshark”, configures dumpcap with setcap, and requires the user to manually add themselves to the “wireshark” group (then log out and log back in to activate it).

```
$ sudo dpkg-reconfigure wireshark-common
$ sudo adduser skarg wireshark
$ exit
```

Don’t do both methods, as they are slightly different solutions.