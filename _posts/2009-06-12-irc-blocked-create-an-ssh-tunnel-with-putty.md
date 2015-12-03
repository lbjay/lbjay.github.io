---
title: IRC Blocked? Create an SSH tunnel with PuTTY
author: lbjay
layout: post
permalink: /archives/83
categories:
  - hacks
tags:
  - proxy
  - putty
  - ssh
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

Can&#8217;t get to IRC because port 6667 is blocked on your local network? Here are some instructions for how to create a SSH tunnel using  [PuTTY][1], and then connect to freenode (or any other IRC server) with [Pidgin][2] using the tunnel as a SOCKS5 proxy. You can most likely *s/Pidgin/your IRC client of choice/*, but the screenshots below will show the Pidgin config dialogs. These instructions also assume that SSH, port 22, is not also blocked. Woe be to you if that is the case.

My original source for how to do this was [this post][3], which describes the same trick but for FireFox.

**Step 1**: create a new PuTTY session configuration. In this case I using the login **me@ssh.example.com** and calling the session **irc-7777**. I usually name the session based on the local port number I&#8217;m going to forward.

<div id="attachment_93" style="width: 466px" class="wp-caption aligncenter">
  <img class="size-full wp-image-93" title="putty1" src="http://blog.reallywow.com/static/uploads/2009/06/putty11.png" alt="create and save a new PuTTY session " width="456" height="435" />
  
  <p class="wp-caption-text">
    create and save a new PuTTY session
  </p>
</div>

**Step 2**: go to the **Connection -> SSH -> Tunnels** node of the session config. In the Source port field enter &#8220;7777&#8221; (or some other port number). In the radio button section below that select **Dynamic** and **Auto**. Click the **Add** button. You should see &#8220;D7777&#8243; appear in the list of forwarded ports.

<div id="attachment_94" style="width: 466px" class="wp-caption aligncenter">
  <img class="size-full wp-image-94" title="putty2" src="http://blog.reallywow.com/static/uploads/2009/06/putty21.png" alt="Configure the ssh tunnel " width="456" height="435" />
  
  <p class="wp-caption-text">
    Configure the ssh tunnel
  </p>
</div>

<div id="attachment_95" style="width: 466px" class="wp-caption aligncenter">
  <img class="size-full wp-image-95" title="putty3" src="http://blog.reallywow.com/static/uploads/2009/06/putty31.png" alt="Tunnel D7777 appears in the list" width="456" height="435" />
  
  <p class="wp-caption-text">
    Tunnel D7777 appears in the list
  </p>
</div>

**Step 3**: go back to the man session config node and save the session again. Then open the PuTTY session by clicking the **Open** button. A normal looking PuTTY terminal window should open. This session is your tunnel so you should probably leave it be. i.e., don&#8217;t use it for doing stuff in the shell and as a tunnel (although I don&#8217;t really know what consequences that would lead to). If the fact that this tunnel takes up space in your TaskBar (it does me) check out [PuTTY-Tray][4].

<div id="attachment_97" style="width: 310px" class="wp-caption aligncenter">
  <img class="size-medium wp-image-97" title="putty4" src="http://blog.reallywow.com/static/uploads/2009/06/putty4-300x150.png" alt="You've probably never seen one of these before" width="300" height="150" />
  
  <p class="wp-caption-text">
    You've probably never seen one of these before
  </p>
</div>

**Step 4**: Configure your Pidgin IRC account to use the tunnel as a SOCKS5 proxy. Go to Accounts -> Manage Accounts. Highlight your IRC protocol account and click Modify (or create one by clicking Add). Go to the Advanced tab of the config dialog. In the Proxy Options section select SOCKS5 as the proxy type, enter &#8220;localhost&#8221; as the Host and &#8220;7777&#8221; (or whatever port you used) as the Port.

<div id="attachment_96" style="width: 314px" class="wp-caption aligncenter">
  <img class="size-full wp-image-96" title="pidgin" src="http://blog.reallywow.com/static/uploads/2009/06/pidgin1.png" alt="Specify your local tunnel as the SOCKS5 proxy" width="304" height="520" />
  
  <p class="wp-caption-text">
    Specify your local tunnel as the SOCKS5 proxy
  </p>
</div>

Save and that&#8217;s it. You should be able to connect to IRC server through Pidgin.

On a *nix machine (or using Cygwin, I suppose) this is, of course, much simpler. You can replace the PuTTY steps with a single ssh command: *ssh -D localhost:7777 me@ssh.example.com*

 [1]: http://www.putty.org/
 [2]: http://www.pidgin.im/
 [3]: http://everythinghurts.com/ssh-tunnelling/
 [4]: http://haanstra.eu/putty/