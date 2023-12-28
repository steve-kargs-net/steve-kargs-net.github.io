---
id: 78
title: 'Character problems after WordPress upgrade on Bluehost'
date: '2007-11-17T17:35:08-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/hosting/character-problems-after-wordpress-upgrade-on-bluehost/'
permalink: /hosting/character-problems-after-wordpress-upgrade-on-bluehost/
categories:
    - hosting
---

[![seal_on_rock](http://steve.kargs.net/wp-content/uploads/2007/thumbs/seal_on_rock_800x600.jpg "seal_on_rock")](http://steve.kargs.net/wp-content/uploads/2007/seal_on_rock_800x600.jpg)I recently upgraded the [WordPress](http://wordpress.org/) install on [BlueHost](http://www.bluehost.com/track/kargsnet/stkblog) at [Kargs.net](http://kargs.net/). The install and upgrade were done using the Fanstastico user interface. After the install, I found that some of the characters in the older postings (mostly the quote character) were shown as unusual characters. After a number of searches, I found the solution.

1\. Modify the wp-config.php by commenting out  
`<br></br>//define('DB_CHARSET', 'utf8');<br></br>//define('DB_COLLATE', '');<br></br>`  
2\. Modify the wp-config-sample.php by commenting out  
`<br></br>//define('DB_CHARSET', 'utf8');<br></br>//define('DB_COLLATE', '');<br></br>`

The second file, wp-config-sample.php, is used to prevent breakage in future upgrades.