---
id: 110
title: 'Convert to MP3 Konqueror Service Menu'
date: '2008-08-05T08:17:22-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=110'
permalink: /linux/convert-to-mp3-konqueror-service-menu/
categories:
    - Linux
    - Music
---

I wanted an easy way to convert music to MP3 from various formats under Konqueror in KDE on Kubuntu Linux. I found an [interesting post about creating a KDE Service Menu](http://ubuntuforums.org/showthread.php?t=684029) which got me started in the right direction. However, I didn’t like the way [ffmpeg](http://ffmpeg.mplayerhq.hu/) converted to 64kbps MP3 quality and the bad sounding results regardless of the bitrate settings that I chose. I tried [lame](http://lame.sourceforge.net/), and was quite pleased with the results. I also didn’t like the way the service menu used the entire filename without stripping the dotted extension, so I copied another service menu [perl example](http://groups.google.co.th/group/alt.comp.lang.perl/browse_thread/thread/dc04e1d8bd91bb35). My “Convert to MP3” service menu script goes into the following location:

```
/usr/share/apps/konqueror/servicemenus/
```

File [convertmp3.desktop](http://steve.kargs.net/wp-content/uploads/2008/08/convert_mp3.desktop):

```
[Desktop Entry]
ServiceTypes=audio/*
Actions=convertToMP3

[Desktop Action convertToMP3]
Name=Convert to MP3
Exec=lame -V2 %f "`echo %f | perl -pe 's/\.[^.]+$//'`.mp3"
```

Enjoy!