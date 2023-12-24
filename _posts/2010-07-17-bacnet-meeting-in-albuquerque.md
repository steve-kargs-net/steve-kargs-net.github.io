---
id: 190
title: 'BACnet Meeting in Albuquerque'
date: '2010-07-17T11:40:27-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=190'
permalink: /bacnet/bacnet-meeting-in-albuquerque/
categories:
    - BACnet
---

I attended the recent [BACnet](http://www.bacnet.org/) meetings in [Albuquerque](http://www.cabq.gov/), and in the process, learned to spell the city name! I participated in the Lighting Applications working group, the Objects and Services working group, the BACnet SSPC, and the MS/TP working group.

[![](http://steve.kargs.net/wp-content/uploads/2010/07/BACnet_Leaders_2010-1024x576.jpg "BACnet Leaders 2010")](http://steve.kargs.net/wp-content/uploads/2010/07/BACnet_Leaders_2010.jpg)

[![](http://steve.kargs.net/wp-content/uploads/2010/07/IMG_1182-150x150.jpg "BACnet Committee meeting, Albuquerque")](http://steve.kargs.net/wp-content/uploads/2010/07/IMG_1182.jpg)[![](http://steve.kargs.net/wp-content/uploads/2010/07/Carl_Neilson-150x150.jpg "Carl Neilson")](http://steve.kargs.net/wp-content/uploads/2010/07/Carl_Neilson.jpg)[![](http://steve.kargs.net/wp-content/uploads/2010/07/IMG_1189-150x150.jpg "Coleman, in the orange shirt")](http://steve.kargs.net/wp-content/uploads/2010/07/IMG_1189.jpg)

One of the proposals that started in the MS/TP working group made it through the public review process, and was voted by our committee to be published!

## The Journey of a Small BACnet Proposal

In [typical bike shed fashion](http://bikeshed.org/), a small change to the BACnet standard took a very long time to become a standard. Here is the story.

In November, 2002, I proposed ([my 13th proposal](http://kargs.net/BACnet/mstp/STK-013-1.pdf)) to expand the allowable baud rates for MS/TP to include 57600 bps and 115200 bps. When reviewing MS/TP in Clause 9, I noticed that the baud rates specified in 9.2.3 are rather limited, and the fastest one doesn’t work well on PC based UARTs (76800 bps). Since PC based control was becoming more prevalent in 2002, it seemed appropriate to permit fast speeds for PC compatible UARTs.

Someone reviewed the proposal, and asked for some data regarding the maximum length of an RS-485 segment while running at 115,200 bps. I searched for the best literature I could find on the subject, and ended up with an[ Application Note from National Instruments](http://www.national.com/an/AN/AN-1057.pdf) which contained a nice graph of Cable Length vs Data Rate for RS-485.

![](http://kargs.net/BACnet/mstp/rs-485_cable_length_data_rate_graph.png "RS-485 Cable Length versus Data Rate graph")

Unfortunately, there was not a table of data along with the graph. I found and quickly learned how to use [Scilab, the free platform for numerical computation.](http://www.scilab.org/) I did some linear interpolation (curve fitting) based on points (red dots) from the graph ([Scilab Script](http://kargs.net/BACnet/mstp/rs485-distance.sce)):

```
-->// Scilab 3.0
-->// data from the graph
-->// The data is linear, but the graph is logarithmic
-->t = [0.1 0.2 0.4 0.5 0.8 1.0];
-->y = [4000 2000 1000 800 500 400];
-->xyd = [t;y];
-->yi=exp(interpln(log(xyd),log(t)));
-->err = (y-yi)'
err  =
1.0D-12 *
!   0.4547474 !
!   0.2273737 !
!   0.2273737 !
!   0.1136868 !
!   0.1705303 !
!   0.1136868 !
-->tt = [0.1 0.1152 0.2 0.2304 0.4 0.4608 0.5 0.8 1.0];
-->yi=exp(interpln(log(xyd),log(tt)));
-->xyi = [tt ; yi]'
xyi  =
!   0.1       4000.     !
!   0.1152    3472.2222 !
!   0.2       2000.     !
!   0.2304    1736.1111 !
!   0.4      1000.      !
!   0.4608    868.05556 !
!   0.5       800.      !
!   0.8       500.      !
!   1.        400.      !
```

Since the graph was logarithmic, the points had to be converted. Scilab took the points (t,y), created a table (xyd), interpolated (yi), checked the error of the curve for each point (err). Then I added some standard baud rates to the list of points (tt), and did the same interpolation. The result is the table (xyi) which includes .1152 (baud rate) at 3472.2222 feet. I de-rated and used 3280 feet (1000 meters) as a safety margin.

I compiled the information into a [revised proposal](http://kargs.net/BACnet/mstp/STK-013-2.pdf), and submitted the information to the working group in October, 2004. At the April, 2005 Germantown meeting, the MS/TP working group [voted this proposal](http://kargs.net/BACnet/mstp/MSTP001.pdf) up to the BACnet SSPC for review and future publication.

The document was discussed again at a subsequent [MS/TP working group](http://groups.yahoo.com/group/bacnet-mstpwg/) meeting in 2006, with concern raised over the reduced distance for the higher baud rate. A consensus vote decided to eliminate 115,200 bps as a possible rate, leaving 57,000. I [revised the proposal](http://kargs.net/BACnet/mstp/STK-013-3.pdf) to that effect in April, 2006, and it was voted up to the full SSPC BACnet Committee for review and future publication.

In October, 2008, there was a discussion of MS/TP baud rates on[ BACnet-L](http://www.bacnet.org/Contact/BACnet-L.htm) mailing list. Coleman indicated that:

> I’d like to get a proposal together that rewords the baud requirements in clause 9 of 135. We’ve discussed 115200 several times in the MS/TP-WG, but I’m thinking something a little less contentious like making 38400 the default and making 9600, 19200, 57600, 76800, and 115200 optional.

[Coleman](http://coleman.jandasoft.biz/) sent a note to me indicating that he had modified the proposal again, mandating that 38400 be a default baud rate in addition to 9600. I checked the venerable “BACnet Document Status Summary” which indicated that my proposal was still in MS/TP working group instead of SSPC. Bummer. It had been sitting around for years due to some missing communication.

I wrote to Coleman and said that I would prefer to leave my original proposal in the SSPC-135 queue as-is since it is more likely to be adopted sooner than later as it is now 3 years in the queue – and a case can be made that it has been sitting there awhile. I suggested that another proposal with the additional mandatory baud rates would be better or could be discussed along with my proposal in the SSPC-135 meeting and added prior to a public review vote by SSPC-135.

My proposal finally made it to the floor of the Atlanta BACnet committee meeting in November, 2009, at the very end of the meeting. After a short discussion, Coleman’s proposal was suggested to replace mine. As meeting time was running out, David Fisher, convener of the MS/TP working group, “passionately insisted that \[Coleman’s proposal\] will get a due amount of serious discussion time in Orlando. This proposal has been delayed unreasonably for years now.”

[Coleman’s proposal](http://kargs.net/BACnet/mstp/CLB-017-2.pdf) was discussed at the next SSPC meeting in Orlando in January, 2010. After a brief discussion and a minor revision, the proposal was voted to Publication Public Review as [Addendum 135-2008ab](<http://kargs.net/BACnet/mstp/Add-135-2008ab-PPR1-Draft _chair-approved_.pdf>). The pubic review period lasted from March 26 to May 10, 2010. It received 2 comments requiring resolution, and 4 supportive comments (which do not require any action to be resolved).

One of the supportive comments suggested that we consider changing MS/TP timing delays when using the 115,200 baud rate in order to provide the fastest possible throughput when using the new speed. It was decided to consider this request, and some analysis was done. When we met in Abuquerque, in June, 2010, the analysis was presented as “no significant speed improvements could be made by changing the time delays.” The BACnet committee voted to approve the public review comment responses, and since there were no substantive changes to the addendum, it is now published as an addendum to the BACnet standard.