---
title: Semweb Gang talks about Glue
author: lbjay
layout: post
permalink: /archives/12
openid_comments:
  - 'a:1:{i:0;s:1:"3";}'
categories:
  - Semantic Web
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

Interesting conversation [this month][1]. (This is the stuff I listen to on my commute.) I was particularly intrigued by the 10 or so minutes spent discussing the need for a method of embedding identifiers and the location of a web service into HTML. Send the identifier to the service and get back the metadata. This is the exact use case of [unAPI][2].

I was all set to get to work and give them a *brrring!* on the cluephone, a.k.a., comment on the post. But before I got around to it [Ed Summers][3] pointed out on irc that you can achieve the same thing using just <link> elements and/or [HTTP Link: headers][4]. In other words, why separate the identifiers from the service URI.

I like how simple unAPI is to implement. Since your metadata service&#8217;s base url doesn&#8217;t change you don&#8217;t have to worry about coordinating attributes of elements that need to appear in both your <head> and page <body>. This is a non-issue for lots of folks, but I bet it&#8217;s not so simple if your using WordPress or Drupal for your CMS.

As for the [Glue extension thingie][5], I&#8217;ll try it out before passing judgement. But it did strike me funny that they&#8217;re not using RDF for anything. Also, and maybe I&#8217;m imagining it, but in the 10-minute wrapup at the end of the podcast I *think* Tom Heath basically takes a some veiled jabs at the Glue guys for being SemWeb poseurs.

 [1]: http://semanticgang.talis.com/2008/12/08/novemberdecember-2008-the-semantic-web-gang-discusses-glue-and-looks-back-at-2008/
 [2]: http://unapi.info
 [3]: http://inkdroid.org
 [4]: http://tools.ietf.org/id/draft-nottingham-http-link-header-03.txt
 [5]: http://getglue.com