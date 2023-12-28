---
id: 132
title: 'GIMP: Removing Noise from Digital Photos'
date: '2008-10-29T10:36:47-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=132'
permalink: /photography/gimp-removing-noise-from-digital-photos/
categories:
    - photography
---

I shot some low light photography at the youth group [Halloween](http://en.wikipedia.org/wiki/Halloween) dance using a Casio Exilim point-n-shoot, and some of the photos had [digital noise](http://en.wikipedia.org/wiki/Image_noise), or [grain](http://en.wikipedia.org/wiki/Film_grain) (as we called it in the days of film).

I searched the internet for some assistance in removing the digital noise using the [GNU Image Manipulation Program (GIMP)](http://gimp.org/), and stumbled upon a well written post about [how to remove digital noise](http://photodoto.com/free-noise-reduction-plugin-for-the-gimp/). The technique makes use of the [GREYCstoration](http://cimg.sourceforge.net/greycstoration/) plugin for the GIMP.

I use the GIMP on [Kubuntu Linux](http://www.kubuntu.org/), and wondered if there was already a package created for GREYCstoration.

```
$ apt-cache search greyc
gimp-plugin-registry - A repository of optional extensions for The GIMP
```

I found it! So I installed it:

```
$ sudo apt-get install gimp-plugin-registry
```

After restarting the GIMP, here are the results:

[![Low light photo (scaled)](http://steve.kargs.net/wp-content/uploads/2008/10/halloweenslowdance-150x150.jpg "halloweenslowdance")](http://steve.kargs.net/wp-content/uploads/2008/10/halloweenslowdance.jpg) Low light photo (scaled)

[![Low light photo (GREYCstoration, scaled)](http://steve.kargs.net/wp-content/uploads/2008/10/halloweenslowdancecropscaled-150x150.jpg "halloweenslowdancecropscaled")](http://steve.kargs.net/wp-content/uploads/2008/10/halloweenslowdancecropscaled.jpg) Low light photo (GREYCstoration, scaled)
