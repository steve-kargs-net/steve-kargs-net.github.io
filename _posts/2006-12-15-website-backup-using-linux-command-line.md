---
id: 60
title: 'Website backup using Linux Command Line'
date: '2006-12-15T11:11:32-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/hosting/website-backup-using-linux-command-line/'
permalink: /hosting/website-backup-using-linux-command-line/
categories:
    - hosting
    - Linux
---

[![easy button](http://steve.kargs.net/wp-content/uploads/2006/12/easybutton.jpg "easy button")](http://steve.kargs.net/wp-content/uploads/2006/12/easybutton.jpg)I needed to backup a website that I run onto [a Linux server in my garage](http://karg.us/), and wondered what the [easy button](http://en.wikipedia.org/wiki/Easy_Button) tool for [Linux](http://www.ubuntu.com/) on the command line would be. Just try searching [Google](http://google.com/) for “Website backup using Linux Command Line” and you don’t get what I was looking for. What I should have searched for was “<span class="txt"><span class="contentpagetitle">Website Mirroring With wget” but I didn’t know what tool I was looking for, remember? As you may have guessed, I finally found [a page full of ads and some outdated command line options for Windows describing how to website mirror with wget](http://www.devarticles.com/c/a/Web-Services/Website-Mirroring-With-wget/). </span></span>

[wget](http://www.gnu.org/software/wget/) is a great tool for website backup, offline browsing, or mirroring as it is known in the server realm. A simple one line command gets you all the files and images that are accessable from the website index and puts them in a directory it creates named after the domain name:

`$ <a href="http://www.gnu.org/software/wget/">wget</a> -mp http://<a href="http://anencephaly.net/">anencephaly.net</a>/`

Yeah! Job accomplished. That was easy, and I didn’t even have to [ask the reindeer](http://www.staples.com/sbd/cre/marketing/centers/holiday_06/agent-mrnibbles.html).