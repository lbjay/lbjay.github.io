---
title: Starting MongoDB on CentOS with NUMA disabled
author: lbjay
layout: post
permalink: /archives/159
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - hacks
tags:
  - centos
  - mongodb
  - numactl
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

This may not be the best way to do this but it works for me. I got fed up with seeing the following message in the logs every time MongoDB was restarted.*

> Wed Aug  1 12:06:39 [initandlisten] ** WARNING: You are running on a NUMA machine.  
> Wed Aug  1 12:06:39 [initandlisten] **          We suggest launching mongod like this to avoid performance problems:  
> Wed Aug  1 12:06:39 [initandlisten] **              numactl &#8211;interleave=all mongod [other options]

I&#8217;m using a pretty boilerplate init.d script for mongo so I figured it would be simple to update the start command to use *numactl*. What I discovered is that my init script uses a builtin bash function called *daemon* to start the mongo process. daemon allows for a &#8211;user option. Unfortunately, *numactl* does not. Neither is it possible to execute a bash function using *numactl*. &#8220;TO THE GOOGLES!&#8221;

Hmm, everything I see recommends wrapping the *numactl* command around another command called *start-stop-daemon*. OK, but CentOS doesn&#8217;t have a *start-stop-daemon* command. Argh.

Finally I resorted to digging into the *daemon* function to see what it was doing and came up with this:

<div class="codecolorer-container text default" style="overflow:auto;white-space:nowrap;width:435px;">
  <div class="text codecolorer">
    numactl --interleave=all runuser -s /bin/bash $MONGO_USER -c "$mongod $MONGO_OPTS"
  </div>
</div>

It works. Moving on now.