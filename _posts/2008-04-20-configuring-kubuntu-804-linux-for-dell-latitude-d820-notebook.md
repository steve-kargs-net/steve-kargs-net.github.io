---
id: 87
title: 'Configuring Kubuntu 8.04 Linux for Dell Latitude D820 Notebook'
date: '2008-04-20T10:28:22-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/linux/configuring-kubuntu-804-linux-for-dell-latitude-d820-notebook/'
permalink: /linux/configuring-kubuntu-804-linux-for-dell-latitude-d820-notebook/
categories:
    - Linux
---

I was pleasantly surprised to have all the hardware working and a smooth install of [Kubuntu](http://kubuntu.com/) 8.04rc for a year old [Dell Latitude](http://dell.com/) D820 notebook PC. There was still a bit of customization to do to make it work like I wanted, but who can fault [Canonical](http://www.canonical.com/) for not knowing what I like?

### Add Codecs, Java, and other Customizations

The official way to do this is documented in the Ubuntu Wiki under [CommonCustomizations](https://wiki.ubuntu.com/CommonCustomizations). There is also a wiki page on [EasyCodecInstallation](https://wiki.ubuntu.com/EasyCodecInstallation). The official meta package is called “ubuntu-restricted-extras” and this installs:

- MP3 playback and decoding
- Sun Java runtime environment
- Flash plugin
- DVD playback
- LAME (to create MP3 compressed audio files)
- msttcorefonts (may be missing in kubuntu extras)
- DeCSS script to download and install for DVD viewing

`$ sudo apt-get install kubuntu-restricted-extras`  
`$ sudo /usr/share/doc/libdvdread3/install-css.sh`  
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

### Get rid of limited use Dolphin

This is one of the main reasons I use Kubuntu and KDE: Konqueror allows me to do many things that Nautilus and Dolphin prevent or are unable to customize  
`$ sudo apt-get remove dolphin`

### Get Rid of IcedTea – Install Sun Java JRE

I had several errors which prevented me from doing useful work on some websites that used Java. Turns out that the default install of Kubuntu used [IcedTea – the OpenJDK](http://iced-tea.org/). Well, apparently it doesn’t mimic Java the way the websites expected, and so, it didn’t work. Into the hopper it goes, and Sun gets the install.  
`$ sudo apt-get remove openjdk-6-jre`  
`$ sudo apt-get install sun-java6-jre`

### Get rid of annoying PC speaker beep

Using a console, remove the PC Speaker driver from the kernel:  
`$ sudo modprobe -r pcspkr`  
Edit **/etc/modprobe.d/blacklist** and add a new line to keep the PC Speaker driver from automatically loading:  
`# Keep the annoying beep from occurring - don't load the PC Speaker driver`  
`blacklist pcspkr`

### Get rid of annoying Synaptic Tap Button

Edit the X11 configuration file `/etc/X11/xorg.conf`

Add the Tapbutton line and any other missing lines in the Synaptic Touchpad section:

`Section "InputDevice"`  
`Identifier  "Synaptics Touchpad"`  
`Driver      "synaptics"`  
`Option      "SendCoreEvents" "true"`  
`Option      "Device" "/dev/psaux"`  
`Option      "Protocol" "auto-dev"`  
`Option      "HorizScrollDelta" "0"`  
`Option      "SHMConfig" "On"`  
`Option      "TapButton1" "0"`  
`EndSection`

You can disable the Tap Button effect immediately using the synclient tool as long as SHMConfig is On:  
`$ synclient TapButton1=0`

### Fix a bug in Firefox 3 rendering Check boxes and Radio boxes

Check boxes and Radio boxes show as a blank box or circle until the focus is moved away. This[ bug was reported](https://bugs.launchpad.net/ubuntu/+source/firefox-3.0/+bug/194624), and the solution is to install a GTK2 engine:  
`$ sudo apt-get install gtk2-engines-qtcurve`

Additionally, go to System Settings-&gt;Appearance-&gt;GTK Styles and fonts, and Set: Use another style = QtCurve.

### Updating a Toshiba A135 Notebook

I also updated our Toshiba A135 Notebook and the sound and sound controls now work! I did have to fix [an fglrx bug to keep from locking up on logout](https://bugs.launchpad.net/ubuntu/+source/linux-restricted-modules-2.6.24/+bug/118605).