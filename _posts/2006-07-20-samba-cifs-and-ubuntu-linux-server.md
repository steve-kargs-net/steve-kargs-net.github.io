---
id: 29
title: 'Samba, CIFS, and Ubuntu Linux Server'
date: '2006-07-20T18:00:08-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/applications/samba-cifs-and-ubuntu-linux-server/'
permalink: /applications/samba-cifs-and-ubuntu-linux-server/
categories:
    - applications
    - Linux
---

![confused](http://steve.kargs.net/wp-content/uploads/2006/07/head.thumbnail.png "confused")I run a couple of servers at my house. One of them is my fileserver, and it uses [Samba](http://www.samba.org/) to do simple Windows filesharing. My 20 GB digital photos partition was full, so I got a 120 GB harddrive and setup an [Ubuntu Server](http://www.ubuntu.com/server/) 6.06 based fileserver. I transferred the files using [rsync](http://samba.anu.edu.au/rsync/), and installed samba on the new server. I set the UID=nobody and the GID=users on all the files. I set the group id inheritance bit on the Linux directories, and removed the world/other rights.

`#!/bin/bash<br></br># files are read/write for group and owner<br></br>find $1 -type f -exec chmod 660 {} \;<br></br># directories are read/write/cd-able/inherited GID<br></br>find $1 -type d -exec chmod 02770 {} \;<br></br># make these files owner=nobody, group=users<br></br>chown -R nobody:users $1`

I setup Samba to mimic the Linux file system, and forced some settings when new files and directories are created. Here is my smb.conf entry:

`[data]<br></br>comment = Common Data Directory<br></br>path = /home/skarg/data<br></br>force user = nobody<br></br>force group = users<br></br>read only = No<br></br>create mask = 0660<br></br>force create mode = 0660<br></br>directory mask = 02770<br></br>force directory mode = 02770<br></br>inherit permissions = Yes<br></br>guest ok = Yes`

Normally, you can add a CIFS mount in /etc/fstab, and specify the UID and GID that the linux filesystem will use. But the cifs filesystem mount wasn’t using the UID that I specified, and that’s when I discovered that Samba now has unix extensions, which cause the problem that I was seeing. Unix extensions can be turned off in samba by adding the following line to /etc/samba/smb.conf:

`[global]<br></br>unix extensions = no`  
I also turned off the extensions on the workstation:

`echo 0 > /proc/fs/cifs/LinuxExtensionsEnabled`

I was trying to get one of the other Ubuntu Server based linux servers to mount the Windows share, but kept getting an error message:

`CIFS VFS: cifs_mount failed w/return code = -22```

Google found the [mailing list where someone had that problem](http://www.nabble.com/Can-only-mount-using-server-IP-!--t1564210.html), and the solution was to add the mount.cifs command, since the kernel didn’t know the domain name to IP lookup. I tried to use the advanced package tool to find it:

`apt-cache search mount.cifs`

Nothing. I tried several other solutions, but they didn’t work. I Googled again, and found [another post about mount.cifs](http://www.archlinux.org/pipermail/arch/2005-November/007401.html), which made me think, and I searched the server for mount.cifs using the [locate](http://www.linuxheadquarters.com/howto/basic/locate.shtml) command. mount.cifs wasn’t there! Finally I went to the [Ubuntu packages site](http://packages.ubuntu.com/), and did a search in the contents of each package. mount.cifs is part of the smbfs package. I initially didn’t want to install the smbfs package since smbfs is depracated in favor of cifs.

`sudo apt-get install smbfs`

Now the server has the CIFS filesystem mounted. However, it is not perfect yet. Stay tuned!