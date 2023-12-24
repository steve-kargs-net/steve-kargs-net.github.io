---
id: 72
title: 'Ubuntu Linux on a Toshiba Laptop'
date: '2007-05-30T00:05:19-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/linux/ubuntu-linux-on-a-toshiba-laptop/'
permalink: /linux/ubuntu-linux-on-a-toshiba-laptop/
categories:
    - Linux
---

[![toshiba KDE desktop](http://steve.kargs.net/wp-content/uploads/2007/toshiba_kde_desktop.thumb.jpg "toshiba KDE desktop")](http://steve.kargs.net/wp-content/uploads/2007/toshiba_kde_desktop.png)I acquired two [Toshiba](http://toshiba.com/) laptops from [a local computer store](http://circuitcity.com/). They were close out models at significantly reduced prices. Their hardware specifications were faster than my existing desktop (Intel(R) Celeron(R) M CPU 430 @ 1.73GHz, 512MB RAM, Radeon Xpress 200M video, SB450 HDA Audio, Atheros wireless, 80GB harddrive, CD/DVD R/W, 3470 bogomips).

I used a [Ubuntu Feisty Linux Live CD](http://www.ubuntu.com/getubuntu/download) to test the functionality of several laptops at the store before I made my decision. I think the two features of the laptop that made it stand out from the others were the Atheros wireless chipset and the ATI Radeon video, both of which have good driver support in Linux. I also looked on the [Ubuntu Laptop Testing project](https://wiki.ubuntu.com/LaptopTestingTeam) for advice before and after I went shopping.

After I got the laptops home, I powered them up and saw [Windows Vista Basic Edition](http://www.windowsvista.com/). Windows Vista was incredibly slow. Apparently it requires a much faster CPU and significantly more RAM. I shrunk the hard disk space and repartitioned under Windows. I rebooted under [Kubuntu Feisty 7.04](http://kubuntu.org/) and installed Linux on the 41GB SDA3 partition. When Kubuntu started I was delighted to see the correct screen resolution and the wireless Ethernet picked up my internet access point using Wireless LAN Manager. The only hardware that was not functioning was the sound card. There was already a bug filed for the [ATI SB450 HD Audio](https://bugs.launchpad.net/ubuntu/+source/alsa-driver/+bug/88570) and some work around solutions, but none of the easy workarounds worked for me. A month later I stumbled upon another [ATI SB450 HD Audio bug](https://bugs.launchpad.net/ubuntu/+source/linux-source-2.6.20/+bug/103379) on [Launchpad.net](http://launchpad.net/), and followed the fix at the end of the thread. Edit the parameters passed to the ALSA driver:

`$ sudo vim /etc/modprobe.d/alsa-base`

Add the following line at the end of the file:

`options snd-hda-intel probe_mask=8 model=3stack`

Save the alsa-base file and restart the computer. After I logged into KDE, I opened the Kmix controls, and enabled the front sound and it worked!

I installed the [ATI graphics accelerator](http://wiki.cchtml.com/). I had to make some edits to the xorg.conf file to get it working. I had to edit the kdmrc file to work around a problem when logging out. I then had accelerated graphics! I updated the [community Wiki installation guide](http://wiki.cchtml.com/index.php/Ubuntu_Feisty_Installation_Guide) with the edits required to make it work.

For the second laptop, I decided that sound was important since I didn’t have the fix yet, and installed Kubuntu Edgy 6.10 Linux. The sound worked, but wireless ethernet did not. Since that was important, I downloaded the latest [MadWifi](http://madwifi.org/) source code, compiled it, installed the driver. I also installed the [Wireless Internet Assistant](http://wlassistant.sourceforge.net/) – a wonderful tool for jumping on a hotspot.

Edit: The[ latest version](http://steve.kargs.net/linux/configuring-kubuntu-804-linux-for-dell-latitude-d820-notebook/) of [Ubuntu](http://ubuntu.com/) / [Kubuntu](http://kubuntu.org/) seems to fix the issues that I had with this Toshiba laptop.