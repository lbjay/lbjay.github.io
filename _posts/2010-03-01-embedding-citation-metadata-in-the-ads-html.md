---
title: Embedding citation metadata in the ADS HTML
author: lbjay
layout: post
permalink: /archives/123
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
openid_comments:
  - 'a:2:{i:0;s:2:"38";i:1;s:2:"39";}'
categories:
  - ADS
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

Here&#8217;s what I know: you can embed a set of <meta/> tags containing citation metadata in your HTML to help Google Scholar to index your content. We&#8217;ve been doing it at [ADS][1] for quite a while. I&#8217;m not certain if the impetus came directly from Google, or, more likely, we got the idea from a [CrossTech blog post][2] by Tony Hammond that describes the technique.

For example, if you execute <code class="codecolorer bash default">&lt;span class="bash">&nbsp;curl &lt;span class="re5">-s&lt;/span> http:&lt;span class="sy0">//&lt;/span>adsabs.harvard.edu&lt;span class="sy0">/&lt;/span>abs&lt;span class="sy0">/&lt;/span>1977NuPhB.126..298A &lt;span class="sy0">|&lt;/span> &lt;span class="kw2">grep&lt;/span> meta&lt;/span></code> you should see:

<div class="codecolorer-container html4strict default" style="overflow:auto;white-space:nowrap;width:435px;height:300px;">
  <div class="html4strict codecolorer">
    ...<br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_language"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"en"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_doi"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"10.1016/0550-3213(77)90384-4"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_abstract_html_url"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"http://adsabs.harvard.edu/abs/1977NuPhB.126..298A"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_title"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"Asymptotic freedom in parton language"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_authors"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"Altarelli, G.; Parisi, G."</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_issn"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"0550-3213"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_date"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"08/1977"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_journal_title"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"Nuclear Physics B"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_volume"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"126"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_firstpage"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"298"</span> <span class="sy0">/</span>></span><br /> <span class="sc2"><<span class="kw2">meta</span> <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"citation_lastpage"</span> <span class="kw3">content</span><span class="sy0">=</span><span class="st0">"318"</span> <span class="sy0">/</span>></span><br /> ...
  </div>
</div>

Since first implementation we&#8217;ve had some back-and-forth with Abhishek Jain at Google Scholar to ensure we&#8217;re making use of the full set of fields that Google Scholar looks for.*

[Dan Chudnov][3], David Bucknum & [Ed Summers][4] at the LoC recently expressed interest in also embedding these tags. In the absence of official reference from the Google Scholar folks, I figured it would be a good thing to post here.

  * citation_language
  * citation_doi
  * citation\_abstract\_html_url
  * citation_title
  * citation_authors
  * citation_issn
  * citation_date
  * citation\_journal\_title
  * citation_volume
  * citation_firstpage
  * citation_lastpage
  * citation_publisher
  * citation_issue
  * citation\_pdf\_url
  * citation_pmid
  * citation_keywords (multiple instances OK)
  * citation_conference
  * citation\_dissertation\_name
  * citation\_dissertation\_institution
  * citation\_patent\_number
  * citation\_patent\_country
  * citation\_technical\_report_number
  * citation\_technical\_report_institution

I had to cull this list via a visual scan of a long, forwarded e-mail thread. So, like I tried to insinuate above, it sure would be great if Google Scholar would publish an official reference to this schema somewhere.

* all instances of the term &#8220;we&#8221; should really be read as &#8220;my boss, Alberto&#8221;.

 [1]: http://ads.harvard.edu
 [2]: http://www.crossref.org/CrossTech/2008/05/natures_metadata_for_web_pages_1.html
 [3]: http://onebiglibrary.net/
 [4]: http://inkdroid.org/journal/