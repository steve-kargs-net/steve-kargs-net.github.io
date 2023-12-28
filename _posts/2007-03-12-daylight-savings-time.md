---
id: 68
title: 'Daylight savings time'
date: '2007-03-12T07:45:42-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/software/daylight-savings-time/'
permalink: /software/daylight-savings-time/
categories:
    - software
---

[![Nightstand and alarm clock](http://steve.kargs.net/wp-content/uploads/2007/thumbs/May18_66.JPG "Nightstand and alarm clock")](http://steve.kargs.net/wp-content/uploads/2007/May18_66.JPG)It’s that time of year again. Time to spring forward. Well, not exactly the same time as last year. The formula for [daylight savings time changed for this year](http://aa.usno.navy.mil/faq/docs/daylight_time.html). That meant that I had to rewrite firmware that used daylight savings time. According to [Wikipedia](http://en.wikipedia.org/wiki/Daylight_saving_time_around_the_world),

> *Beginning in 2007, DST will start on the second Sunday in March (March 11, 2007), and change back to standard time on the first Sunday in November (November 4, 2007). Under Section 110 of the Energy Policy Act of 2005, the U.S. Department of Energy is required to study the impact of the DST extension no later than nine months after the change takes effect. Congress has retained the right to revert to the DST schedule set in 1986 if it cannot be shown that there are significant energy savings from an extension of DST or if the extension may prove to be unpopular with the American public. One potential issue is that some northern regions on the western edge of time zones will for the first time since the 1974-75 “almost year round” DST experiment have sunrise times that occur after 8am.*

In two of my controllers I use, the built in hardware clock of the PC/104 card automatically handles the daylight savings time change. I simply set a bit and it would automatically spring forward or fall back. Well, almost. One of the controllers used a realtime clock chip by Odin which didn’t come out of daylight savings time and got stuck at 1am on the last Sunday of October. Since I could no longer utilize the hardware clock, I had to handle the daylight savings time change in software. There were two cases that I needed to cover. The first case is handling the timer interrupt and springing forward one hour or falling back one hour. The timer interrupt code turned out to be much simpler than I first thought. It is a good thing to be simple in an interrupt. Here is part of the code:

<div class="dean_ch" style="white-space: wrap;">1. <div class="de1">span class=”coMULTI”&gt;/* begin DST – Second Sunday in March */ <span class="coMULTI">/\* ANSI is months since January \*/</span><span class="coMULTI">/\*March\*/</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="br0">(</span>data.<span class="me1">tm\_wday</span> == <span class="nu0">1</span> <span class="coMULTI">/\*Sunday\*/</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="br0">(</span>data.<span class="me1">tm\_mday</span> &gt;= <span class="nu0">8</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="coMULTI">/\* second Sunday \*/</span> <span class="br0">(</span>data.<span class="me1">tm\_mday</span> &lt;= <span class="nu0">14</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="br0">(</span>data.<span class="me1">tm\_hour</span> == <span class="nu0">2</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="coMULTI">/\* 2:00 am \*/</span> <span class="br0">(</span>data.<span class="me1">tm\_min</span> == <span class="nu0">0</span><span class="br0">)</span> &amp;amp;&amp;amp; <span class="br0">(</span>data.<span class="me1">tm\_sec</span> == <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span> <span class="coMULTI">/\* do something here \*/</span> <span class="br0">}</span><span class="br0">}</span></div>

</div>The second case was to determine if the date and time was during daylight savings time or not. This is used when the date and time get set on the controller, and to display the daylight savings time status. The code is more complex than the interrupt routine. Here is part of the code:

<div class="dean_ch" style="white-space: wrap;">1. <div class="de1">span class=”coMULTI”&gt;/* simple bounds check */<span class="coMULTI">/\* get the start date for DST – Second Sunday in March \*/</span></div>Testing the Daylight Savings Time algorithm was fairly routine using Unit Testing:
    
    <div class="dean_ch" style="white-space: wrap;">
    1. <div class="de1">span class=”coMULTI”&gt;/* original DST */<span class="coMULTI">/\* new for 2007 DST \*/</span></div>Hope you are getting used to waking up earlier!
    
    </div>

</div>