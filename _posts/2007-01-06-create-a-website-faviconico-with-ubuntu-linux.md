---
id: 64
title: 'Create favicon.ico with Ubuntu Linux'
date: '2007-01-06T09:25:58-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/hosting/create-a-website-faviconico-with-ubuntu-linux/'
permalink: /hosting/create-a-website-faviconico-with-ubuntu-linux/
categories:
    - clipart
    - hosting
    - Linux
---

I was interested in creating a [favicon.ico](http://en.wikipedia.org/wiki/Favicon) file in [Ubuntu Linux](http://www.ubuntu.com/) for a [new website that I helped create](http://bouncesbybob.com/). I recalled having used KIconEdit to do it before. I installed KIconEdit and used that to create the icon. However, KIconEdit did not have any options to save as favicon.ico. I turned to the internet for help.

Most of the information gleened by [Google search](http://google.com/) said to save the file as a 16×16 pixel [PNG file](http://en.wikipedia.org/wiki/PNG), and use one of the icon command line tools to convert it to the favicon.ico format. So I looked in [apt-get](http://en.wikipedia.org/wiki/Advanced_Packaging_Tool) cache to see if any icon tools were available.

`$ apt-cache search favicon<br></br>icoutils - Create and extract MS Windows icons and cursors`

Yeah! That looked promising. So I install icoutils using [apt-get](http://en.wikipedia.org/wiki/Advanced_Packaging_Tool).

`$ sudo apt-get install icoutils`

Wow! That was easy! Now how do I use this tool? Well, [man pages](http://en.wikipedia.org/wiki/Manual_page_%28Unix%29) usually help.

`$ man icoutils<br></br>No manual entry for icoutils`

Bummer! Well, maybe the package will give me some clues.

`$ apt-cache show icoutils<br></br>Package: icoutils<br></br>Status: install ok installed<br></br>Priority: optional<br></br>Section: graphics<br></br>Installed-Size: 172<br></br>Maintainer: Colin Watson<br></br>Architecture: i386<br></br>Version: 0.25.0-1<br></br>Depends: libc6 (>= 2.3.4-1), libpng12-0 (>= 1.2.8rel), zlib1g (>= 1:1.2.1), perl, libwww-perl<br></br>Suggests: libterm-readline-gnu-perl | libterm-readline-perl-perl<br></br>Description: Create and extract MS Windows icons and cursors<br></br>Icoutils is a set of programs that deal with MS Windows icons and cursors. Resources such as icons and cursors can be extracted from MS Windows executable and library files with "wrestool". Conversion of these files to and from PNG images is done with "icotool". "extresso" automates these tasks with the help of special resource scripts.<br></br>.<br></br>This package can be used to create "favicon.ico" files for web sites.`

Aha! I could potentially use icotool to convert the PNG icon to a favicon. icotool had both a man page and a `--help` option. I used icotool on the command line to convert my PNG file.

`$ icotool -o favicon.ico -c favicon.png`

[![maryfeet.jpg](http://steve.kargs.net/wp-content/uploads/2007/thumbs/maryfeet.jpg "maryfeet.jpg")](http://steve.kargs.net/wp-content/uploads/2007/maryfeet.jpg)I also used [The GIMP](http://gimp.org/) image tool to convert a [JPEG](http://en.wikipedia.org/wiki/JPEG) scan of my daughter Mary Elizabeth’s footprints to a PNG. I opened the image, scaled it to 16×16 pixels, and saved it as favicon.png. I used icotool to convert the PNG file to a favicon.ico file. I uploaded the favicon.ico file to her memorial website [anencephaly.net](http://anencephaly.net/).