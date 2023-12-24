---
id: 285
title: 'BACnet Committee Meets in San Francisco'
date: '2012-06-05T18:07:48-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=285'
permalink: /bacnet/bacnet-committee-meets-in-san-francisco/
categories:
    - BACnet
    - travel
---

Our [BACnet](http://www.bacnet.org/) committee and working groups met in San Francisco in May, 2012. It was fun to see friends, enjoy some cool weather, and eat some good food in a big city.

[![](http://steve.kargs.net/wp-content/uploads/2012/06/ritter-isler-robin-os-wg-2012-150x150.jpg "ritter-isler-robin-os-wg-2012")](http://steve.kargs.net/wp-content/uploads/2012/06/ritter-isler-robin-os-wg-2012.jpg)[![BACnet meetin in SF at PGE](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0765-150x150.jpg "BACnet meeting in SF at PGE")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0765.jpg)[![BACnet meeting in SF at PGE](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0768-150x150.jpg "BACnet meeting in SF at PGE")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0768.jpg)

Next door to Pacific Gas and Electric, our host, is a restaurant called [Buca di Beppo](http://www.bucadibeppo.com/), an Italian restaurant known for its large portions and eccentric decor. We had lunch at one of the specialty tables – a “Pope’s Table” that seats 12-18.

[![](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0795-150x150.jpg "Buca")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0795.jpg)[![](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0773-150x150.jpg "Buca Pope Room")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0773.jpg)[![](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0771-150x150.jpg "Buca BACnet")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0771.jpg)

One night, our group was feeling adventuresome, and loaded onto [BART](http://www.bart.gov/) to find an infamous San Francisco dining establishment called [Rosamunde Sausage Grill](http://rosamundesausagegrill.com/).

[![](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0805-300x179.jpg "BART")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0805.jpg)[![](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0803-150x150.jpg "IMAG0803")](http://steve.kargs.net/wp-content/uploads/2012/06/IMAG0803.jpg)

A lot of our proposals had gone out for public review in the Spring, and so we had to create comment responses to any of the comments received. Some of the proposals sailed through the public review process without needing any substantive changes, which mean they will go to ASHRAE and be reviewed and approved for publication.

## BACnet Property\_List property

One of the new items that made it through publication was the Property\_List property, which will be added to all objects for the new revision of BACnet. I proposed this little gem in 2007, and it was met with stiff resistance by those developing XML to describe BACnet devices. The pundits said that if we introduced the Property\_List property, everyone would use it instead of XML, and that we should wait until XML and the Application Profiles working group completed their work. The proposal was tabled for a couple years, but came to life again during the Objects and Services working group meetings. A few tweaks were made to the [STK-026](http://steve.kargs.net/wp-content/uploads/2012/06/STK-026-1.pdf) proposal, and [Add-135-2010ao](http://www.bacnet.org/Addenda/Add-135-2010ao-PPR1-draft-1_chair_approved.pdf) was ready for public review.

> **12.x.X Property\_List**  
> This read only property is a BACnetARRAY of property identifiers, one property identifier for each property that exists within the object. The Object\_Name, Object\_Type, Object\_Identifier, and Property\_List properties are not included in the list.

Additionally, from the ReadPropertyMultiple specification:

> The Property\_List property shall not be returned when properties ALL or REQUIRED are requested.

Pretty simple, but pretty powerful for being able to discover all the properties in all the objects in a device. One of the comments received in public review summed up our sentiments:

> Property\_List is a very good addition. If someone had thought of this in 1995, we could have avoided the evil “ALL” property. However, since this property is “required”, but didn’t previously exist, and since it is likely to be widely used, it is worth flagging the protocol revision at which it is introduced.

The Protocol\_Revision hasn’t been issued yet for this change, since the enumerations and other numbers associated with the published specification are no longer created when the proposals are going through the public review process.