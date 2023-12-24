---
id: 63
title: 'USB Drive Read-Only'
date: '2006-12-18T09:23:22-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/linux/usb-drive-read-only/'
permalink: /linux/usb-drive-read-only/
categories:
    - Linux
---

[![trio_mp3_player.jpg](http://steve.kargs.net/wp-content/uploads/2006/12/.thumbs/.trio_mp3_player.jpg "trio_mp3_player.jpg")](http://steve.kargs.net/wp-content/uploads/2006/12/trio_mp3_player.jpg)I was in a hurry on Sunday as our family was about to leave on a road trip to visit some relatives. Joshua had a problem copying some music from his [Kubuntu Linux](http://kubuntu.org/) PC to an MP3 player that I have because the MP3 player was full. I had purchased the 512MB Trio MP3 player from [eCost](http://www.ecost.com/), one of my favorite discount online stores. I have used the MP3 player on many airline trips.  
Joshua tried to delete the existing files on the MP3 player but his [KDE Konqueror](http://www.konqueror.org/) file manager window said that the files could not be deleted since the files were read-only. I had put the files on there with my [Ubuntu Linux](http://www.ubuntu.com/) PC. Why couldn’t he use the USB drive?

I took over at his keyboard and attempted to remount the Trio USB thumb drive MP3 player as read-write:

`$ mount -o remount,rw -t vfat /dev/sdb1 /media/sdb`

[mount](http://en.wikipedia.org/wiki/Mount_%28computing%29) refused replying that it could not mount the read-only file system as read-write. Maybe the drive was corrupted or something. I searched the internet for some [information on fixing the filesystem of a USB flash drive](http://linuxactivist.blogspot.com/2006/08/linux-tip-resurrecting-broken-usb.html). Then I tried to repartition and reformat:

`$ fdisk /dev/sdb`

I entered the [fdisk utility](http://en.wikipedia.org/wiki/Fdisk) as read-only and knew then that fdisk was not going to work. By this time I was really frustrated and it was time to leave. Why wouldn’t Linux allow me to delete the existing files or partition or format? We left the house without the music and began the trip. I was deep in thought about this perplexing issue.

![trio_mp3_hold.jpg](http://steve.kargs.net/wp-content/uploads/2006/12/trio_mp3_hold.jpg "trio_mp3_hold.jpg")Then an idea came to me about half way to our destination. The Trio MP3 player has a HOLD button that I use to keep the keys from being pressed while it is in my pocket. I began to suspect that the hold button was preventing the USB flash drive files from being deleted. When we returned home, I moved the HOLD button, and inserted the Trio MP3 thumb drive into my Linux PC. I selected a music file and deleted it. Success! The drive had automatically mounted as read-write, and I could add and remove files at will. [PEBKAC](http://en.wikipedia.org/wiki/PEBKAC)!