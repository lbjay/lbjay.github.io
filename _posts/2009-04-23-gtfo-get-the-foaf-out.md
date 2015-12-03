---
title: 'gtfo: get the foaf out'
author: lbjay
layout: post
permalink: /archives/74
categories:
  - code4lib
  - foaf
  - Linked Data
tags:
  - bcb4
  - code4lib
  - foaf
  - linkeddata
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

Leading up to the [Linked Data pre-conf][1] at [cod4lib09][2] there were several [irc][3] discussions around just how to structure the day and what could we do to give attendees the best shot at having an &#8220;ah-ha moment&#8221;. One idea was to create a simple application that would demonstrate the potential of linked data while also being participatory. I think it took [Ed Summers][4] less than 24 hours to hack together the first iteration of the cod4lib2009 attendees foaf crawler/gallery [thingy][5]. He can usually be counted on for such feats of overnight engineering.

<!--more-->By the day of the pre-conf we already had a gallery of 20+ foaf profiles. I spent part of the afternoon that day trying to guide several folks through the process of creating a foaf file and getting linked into our new corner of the web of data (with varying degrees of success). Along the way several people added enhancements, bugs were identified and sometimes fixed, much was learned re: linked data, vocabs, 

[hash fragments vs. 303s][6], etc. [Jonathan Brinley][7] and [Michael Klein][8] even wrote a companion [Supybot plugin][9] for our irc bot, [zoia][10]. It was fun.

Since then my mind has come back to it now and then, mulling over how simple it would be to push some of the variables into a configuration file and make the crawler + gallery re-usable for other events, for example, the soon-to-be-happening [BarCampBoston 4][11]. This turned out to be relatively easy, and pretty quickly I had an [demo attendees page][12] for bcb4. Some fellow bcb4 goers were nice enough to participate by them asserting their attendence in their FOAF files and me pretending to know them. I&#8217;ve decided not to try leading any sessions on linked data or foaf at bcb4, mostly because it&#8217;s my first time and I want to soak up what other folks are into, but maybe it&#8217;ll make for a good ice-breaker or something.

Here&#8217;s my problem though: I&#8217;m starting to second guess myself as to the level of general usefulness of this thing&#8211;which, btw, I have christened **gtfo**, aka &#8220;gitfo&#8221;, aka &#8220;get the foaf out&#8221;&#8211;outside of the context of a tutorial/demo. I mean, could it really even function as an actual conference event attendee gallery? There&#8217;s the whole issue of folks needing to foaf:knows each other. I feel like there&#8217;s the seed of something cool in there, but it may need a substantial rethink and refactor to get beyond being the equivalent of the pet store shopping cart of linked data apps.

I have a few ideas&#8230; like allowing the criteria for inclusion to be configurable as something other than attendance at a specified event&#8230; or allowing the crawler to traverse a network of people connected via [DOAP][13] assertions rather than foaf:knows&#8230; or maybe allowing for galleries generated dynamically based on user input rather than a passive crawler, e.g., 1) choose seed node, 2) choose link relationship, 3) choose inclusion criteria, 4) generate gallery.

Anyway, if you&#8217;re interested in contributing ideas and or code, I&#8217;ve pushed my fork of the original app to Github: <http://github.com/lbjay/gtfo/tree/master>.

 [1]: http://wiki.code4lib.org/index.php/LinkedData
 [2]: http://code4lib.org/conference/2009/
 [3]: http://code4lib.org/irc
 [4]: http://inkdroid.org
 [5]: http://inkdroid.org/c4l2009/attendees
 [6]: http://www.w3.org/2001/tag/issues.html#httpRange-14
 [7]: http://xplus3.net/
 [8]: http://twitter.com/mbklein
 [9]: http://svn.breaksalot.org/supybot-plugins/plugins/FOAF/
 [10]: http://www.code4lib.org/id/zoia
 [11]: http://www.barcampboston.org/
 [12]: http://reallywow.com/bcb4/attendees
 [13]: http://trac.usefulinc.com/doap