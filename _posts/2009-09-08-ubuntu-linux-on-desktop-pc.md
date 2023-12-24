---
id: 163
title: 'Ubuntu Linux on Desktop PC'
date: '2009-09-08T20:47:12-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=163'
permalink: /software/ubuntu-linux-on-desktop-pc/
categories:
    - applications
    - Linux
    - software
---

I refurbished a couple of PCs for my family to use, and installed the latest Ubuntu Linux on them – Ubuntu 9.04 Jaunty. I also updated my dual boot work computer with the latest Ubuntu – it was running Kubuntu and the latest Kubuntu is just foreign to me.

As is usually the case, adding additional packages is essential to getting the computer working right for me.

### Add Codecs, Java, and other Customizations

The official way to do this is documented in the Ubuntu Wiki under [CommonCustomizations](https://wiki.ubuntu.com/CommonCustomizations). There is also a wiki page on [EasyCodecInstallation](https://wiki.ubuntu.com/EasyCodecInstallation). The official meta package is called “ubuntu-restricted-extras” and this installs:

- MP3 playback and decoding
- Sun Java runtime environment
- Flash plugin
- DVD playback
- LAME (to create MP3 compressed audio files)
- msttcorefonts (may be missing in kubuntu extras)
- DeCSS script to download and install for DVD viewing

`$ sudo apt-get install ubuntu-restricted-extras`  
`$ sudo /usr/share/doc/libdvdread4/install-css.sh`  
`$ sudo apt-get install msttcorefonts`

### Add the ability to compile, edit, and maintain code

Here are the compilers and their documents  
`$ sudo apt-get install build-essential subversion-tools  gcc-4.2-doc glibc-doc manpages-dev`  
`$ sudo apt-get install mingw32 mingw32-binutils mingw32-runtime`  
I need access to subversion and XSLT ChangeLog tools  
`$ sudo apt-get install subversion-tools`  
`$ sudo apt-get install xsltproc`  
I install a couple of editors, useful for various things. Kate is already installed.  
`$ sudo apt-get install scite`  
`$ sudo apt-get install vim-full`  
Useful tools for cleaning up code, converting comments and line endings, and code statistics:  
`$ sudo apt-get install splint`  
`$ sudo apt-get install sloccount`  
`$ sudo apt-get install indent`  
`$ sudo apt-get install liwc`  
`$ sudo apt-get install tofrodos`

### Add favorite online music source and music/video player VLC

`$ sudo apt-get install streamtuner`  
`$ sudo apt-get install vlc`

### Add the Adobe Flash Plugin and Sun Java JRE

A lot of websites use Flash or Java for their user interface, so it seems that they are essential.

`$ sudo apt-get install adobe-flashplugin``<br></br>$ sudo apt-get install sun-java6-jre`

### Get rid of annoying PC speaker beep

Using a console, remove the PC Speaker driver from the kernel:  
`$ sudo modprobe -r pcspkr`  
Create **/etc/modprobe.d/blacklist-user.conf** and add a line to keep the PC Speaker driver from automatically loading:

`# Keep the annoying beep from occurring``<br></br># don't load the PC Speaker driver`  
`blacklist pcspkr`

## [SynapticsTouchpad](https://help.ubuntu.com/community/SynapticsTouchpad)

The laptop has a touchpad, which is really annoying when you also have a USB mouse attached, because the touchpad picks up thumps made by my big fingers and makes the mouse click somewhere that you didn’t want it to click. Correcting this in Ubunut Jaunty is as easy as selecting **System &gt; Preferences &gt; Mouse**, under the Touchpad tab. Uncheck the **Enable mouse clicks with touchpad** check box.