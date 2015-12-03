---
title: 'My &#8220;unified&#8221; twitter + identi.ca client'
author: lbjay
excerpt: "I've been on the lookout for a client that would somehow unify my streams from both Twitter & Identi.ca. There's several clients that will support one-or-the-other, but not both simultaneously. My solution doesn't technically do this either but it scratches my itch to at least have them in the same window."
layout: post
permalink: /archives/22
categories:
  - identi.ca
  - microblogging
  - twitter
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

I&#8217;ve been on the lookout for a client that would somehow unify my streams from both [Twitter][1] & [Identi.ca][2]. There&#8217;s a few clients that will support one-or-the-other (sometimes via [hacking the source][3]) but I&#8217;ve found none that scratch my itch of have both services presented in the same window. My taskbar is precious real-estate.

These instructions reflect my setup on an Ubuntu vhost which I ssh into via PuTTY.

Required:

  * Twitter account
  * Identi.ca account
  * [TTYtter][4], a perl command-line client for accessing Twitter-compatible APIs
  * Gnu Screen

Step 1, download TTYtter, make it executable and put it somewhere on your $PATH.

Step 2, create a file at ~/.ttytterrc1 with the following contents, including your identi.ca login:

<pre><span style="color: #000080;">  url=http://identi.ca/api/statuses/friends_timeline.json
  rurl=http://identi.ca/api/statuses/replies.json
  uurl=http://identi.ca/api/statuses/user_timeline
  wurl=http://identi.ca/api/users/show
  update=http://identi.ca/api/statuses/update.json
  dmurl=http://identi.ca/api/direct_messages.json
  frurl=http://identi.ca/api/friendships/exists.json
  user=[username]:[pass]
</span></pre>

Step 3, create another file at ~/.ttytterc2 with just your twitter login:

<pre><span style="color: #000080;">user=[username]:[pass]</span></pre>

Step 4, create a dedicated screen session with the command **<span style="color: #000080;">screen -S ttytter</span>**

Step 5, split the screen horizontally using the screen command **<span style="color: #000080;">Ctrl+a S</span>**

Step 6, start your Identi.ca session in the top window with the command <span style="color: #000080;"><strong>ttytter.pl -rc=1</strong></span>

Step 7, switch to the bottom pane with the screen command <span style="color: #000080;"><strong>Ctrl+a TAB</strong></span>

Step 8, create a new window in the bottom pane with the screen command **<span style="color: #000080;">Ctrl+a c</span>**

Step 9, start the Twitter session in the bottom pane with the command <span style="color: #000080;"><strong>ttytter.pl -rc=2</strong></span>

<div id="attachment_25" style="width: 310px" class="wp-caption alignnone">
  <a href="http://blog.reallywow.com/wp-content/uploads/2009/01/ttytter.png"><img class="size-medium wp-image-25" title="ttytter" src="http://blog.reallywow.com/wp-content/uploads/2009/01/ttytter-300x267.png" alt="Example screenshot" width="300" height="267" /></a>
  
  <p class="wp-caption-text">
    Example screenshot
  </p>
</div>

Only set this up 2 hours ago but already I can tell this is going to work for me long term. Beats having to do hard resets due to some combination of [Twhirl][5] and/or my video drivers. One improvement I&#8217;d like to investigate is some kind of color highlighting of the <username>&#8217;s to improve readability.

*Update: January 13, 2009 at 11:30*

So I quickly realized that the above setup has a major malfunction, namely that it doesn&#8217;t allow preserving of the split window so it&#8217;s not possible to detach and reattach to the ttytter screen session. So there&#8217;s an extra trick necessary to do this:

Step 3.5, create an &#8220;outer&#8221; screen session that wraps the ttytter session with the command <span style="color: #000080;"><strong>screen -e^Ee -S outer</strong></span>.

The **-e^Ee** option binds the escape key for that session to Ctrl+e instead of the default Ctrl+a. This is a common trick for embedding screen sessions within sessions. With this extra step I can now detach from the outer session using <span style="color: #000080;"><strong>Ctrl+e d</strong></span> and reattach with the inner split-screen session presevered using **<span style="color: #000080;">screen -r outer</span>**.

Also, I learned that to colorize the output you can use the -ansi option to ttytter.

 [1]: http://twitter.com/lbjay
 [2]: http://identi.ca/lbjay
 [3]: http://hg.mozilla-hispano.org/uncryptic/identifox/overview/
 [4]: http://www.floodgap.com/software/ttytter
 [5]: http://www.twhirl.org/