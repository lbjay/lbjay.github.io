---
title: Exploring Astronomy Dataset Links with GridWorks
author: lbjay
layout: post
permalink: /archives/135
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - ADS
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

At [ADS][1] we are looking at new ways to index and provide full text searching for the Astronomy and Physics literature we manage to obtain, either through scanning + OCR of historical content, or from digital material provided by some publishers. Two options we&#8217;re looking at are [Apache Solr][2] and [CDS-Invenio][3]. But that&#8217;s not what this post is about.

While parsing and indexing a pile of about 42k articles from the past dozen or so years of the [ApJ][4], [AJ][5], [ApJL][6] and [ApJS][7], formatted in the [NLM XML schema][8], I noticed that many of the articles contained external links to various things, most interestingly, astronomical datasets.* My first thought was, &#8220;hmm, I wonder what&#8217;s at the other end of all those links&#8230;,&#8221; followed closely by, &#8220;hey, crawling those links would make a nice dataset to load into that nifty new [Freebase Gridworks][9] tool I heard about the other day.&#8221; So that&#8217;s what I did.

Out of 13652 articles there were 33600 total links which fell into three categories: http urls (28555), dataset links (938) and supplement links (4107). Dataset links consist of an identifier that looks something like *ADS/Sa.CXO#obs/927*. To get the goods you have to feed that id to a [resolver][10] which, assuming a [valid][11] identifier, will redirect you to the [real location][12] of the dataset. Supplement links took a bit more head-scratching as their values consisted of just a relative file name, like *datafile3.txt* or *69491.figures.html*. We figured out that the solution was to append the filename to the publisher&#8217;s URL for the article, e.g., [article][13] and [dataset][14] or [article][15] and [figures][16].

The ultimate objective was to load the results of crawling these links into Gridworks, but that means getting the data into csv or tsv form. Rather than have the crawl script output straight to csv, I stash the results in a [MongoDB][17] instance. Here&#8217;s an example of one of the resulting json documents in Mongo:

<div class="codecolorer-container javascript default" style="overflow:auto;white-space:nowrap;width:435px;height:300px;">
  <div class="javascript codecolorer">
    <span class="br0">&#123;</span>u<span class="st0">'_id'</span><span class="sy0">:</span> ObjectId<span class="br0">&#40;</span><span class="st0">'4bfc3737a1f714263b000012'</span><span class="br0">&#41;</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'anchor_text'</span><span class="sy0">:</span> u<span class="st0">'http://astronomy.swin.edu.au/staff/dforbes/glob.html'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'bibcode'</span><span class="sy0">:</span> u<span class="st0">'2001ApJ...556L..83F'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'content'</span><span class="sy0">:</span> u<span class="st0">'<HTML><span class="es0">\n</span><HEAD><span class="es0">\n</span><TITLE>Duncan A. Forbes, Swinburne University, Globular Clusters</TITLE><span class="es0">\n</span></HEAD><span class="es0">\n</span><span class="es0">\n</span><h1> Globular Cluster Research</h1><span class="es0">\n</span><span class="es0">\n</span>I am interested in various aspects of Extragalactic Globular<span class="es0">\n</span> &nbsp; &nbsp;Cluster research. In particular the formation and evolution<span class="es0">\n</span> &nbsp; &nbsp;of Globular Cluster Systems and their host galaxies. <span class="es0">\n</span><br><span class="es0">\n</span><span class="es0">\n</span><UL><span class="es0">\n</span><A HREF="colours.html">GLOBULAR CLUSTER PHOTOMETRY DATABASE</A><span class="es0">\n</span></UL><span class="es0">\n</span><span class="es0">\n</span><UL><span class="es0">\n</span><A HREF="spectra.html">GLOBULAR CLUSTER SPECTRAL DATABASE</A><span class="es0">\n</span></UL><span class="es0">\n</span><span class="es0">\n</span><span class="es0">\n</span><UL><span class="es0">\n</span><A HREF="review.html">GLOBULAR CLUSTER REVIEW PAPERS</A><span class="es0">\n</span></UL><span class="es0">\n</span><span class="es0">\n</span><span class="es0">\n</span><UL><span class="es0">\n</span><A HREF="http://www.ucolick.org/~brodie/Sages/sages.html"> SAGES PROJECT</A><span class="es0">\n</span></UL><span class="es0">\n</span><span class="es0">\n</span><UL><span class="es0">\n</span><A<span class="es0">\n</span><span class="es0">\t</span> &nbsp;HREF="http://www.physics.mcmaster.ca/resources/fs3_resources.html"> HARRIS DATABASE</A><span class="es0">\n</span></UL><span class="es0">\n</span><span class="es0">\n</span><span class="es0">\n</span><span class="es0">\n</span><tr><td><hr noshade></td></tr><span class="es0">\n</span><span class="es0">\n</span> </BODY><span class="es0">\n</span>'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'context'</span><span class="sy0">:</span> u<span class="st0">'<p>The combined sample data are available at <ext-link ext-link-type="uri" xlink:href="http://astronomy.swin.edu.au/staff/dforbes/glob.html">http://astronomy.swin.edu.au/staff/dforbes/glob.html</ext-link>. </p><span class="es0">\n</span>'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'doi'</span><span class="sy0">:</span> u<span class="st0">'10.1086/323006'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'ft_source'</span><span class="sy0">:</span> u<span class="st0">'/proj/ads/articles/sources/AAS/ApJL/2001/556/2/323006/323006.xml'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'link_id'</span><span class="sy0">:</span> u<span class="st0">'http://astronomy.swin.edu.au/staff/dforbes/glob.html'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'link_type'</span><span class="sy0">:</span> u<span class="st0">'UrlLink'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'response'</span><span class="sy0">:</span> <span class="br0">&#123;</span>u<span class="st0">'accept-ranges'</span><span class="sy0">:</span> u<span class="st0">'bytes'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'content-length'</span><span class="sy0">:</span> u<span class="st0">'781'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'content-location'</span><span class="sy0">:</span> u<span class="st0">'http://astronomy.swin.edu.au/~dforbes/glob.html'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'content-type'</span><span class="sy0">:</span> u<span class="st0">'text/html; charset=UTF-8'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'date'</span><span class="sy0">:</span> u<span class="st0">'Tue, 25 May 2010 10:14:07 GMT'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'server'</span><span class="sy0">:</span> u<span class="st0">'Apache/2.2.15 (Unix) DAV/2 mod_ssl/2.2.15 OpenSSL/0.9.8e-fips-rhel5'</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;u<span class="st0">'status'</span><span class="sy0">:</span> u<span class="st0">'200'</span><span class="br0">&#125;</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'solr_id'</span><span class="sy0">:</span> u<span class="st0">'31908'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'url'</span><span class="sy0">:</span> u<span class="st0">'http://astronomy.swin.edu.au/staff/dforbes/glob.html'</span><span class="sy0">,</span><br /> &nbsp;u<span class="st0">'xpath'</span><span class="sy0">:</span> u<span class="st0">'/html/article/body/sec[5]/fn-group/fn/p/ext-link'</span><span class="br0">&#125;</span>
  </div>
</div>

From there it was easy to dump what I needed to csv and load into Gridworks. I&#8217;m not going to get into how totally awesome the Gridworks software is, except to say you should watch the [demo videos][18].

I can&#8217;t post the entire Gridworks project, but here&#8217;s some screencaps, a column list and some of the more interesting facets.

<p style="text-align: center;">
  <div id="attachment_147" style="width: 310px" class="wp-caption aligncenter">
    <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks.png"><img class="size-medium wp-image-147 " title="gridworks" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks-300x191.png" alt="" width="300" height="191" /></a>
    
    <p class="wp-caption-text">
      Initial data load plus some derived columns
    </p>
  </div>
  
  <p>
    Column list:
  </p>
  
  <ul>
    <li>
      Id of the MongoDB doc
    </li>
    <li>
      Id of the solr doc
    </li>
    <li>
      ADS bibcode identifier of the article
    </li>
    <li>
      Publication year &#8211; derived from the bibcode
    </li>
    <li>
      DOI
    </li>
    <li>
      xpath expression of the <ext-link> element
    </li>
    <li>
      parent tag &#8211; the containing element type
    </li>
    <li>
      link context &#8211; the containing element&#8217;s serialized xml contents
    </li>
    <li>
      link type &#8211; one of url, dataset or supplement
    </li>
    <li>
      anchor text &#8211; the text contents of the <ext-link>
    </li>
    <li>
      full text source file
    </li>
    <li>
      journal
    </li>
    <li>
      full text source &#8211; publisher
    </li>
    <li>
      extlink id &#8211; either the url or the dataset id or the supplement filename
    </li>
    <li>
      domain &#8211; derived from the url
    </li>
    <li>
      status &#8211; http status returned when requesting the resource
    </li>
    <li>
      content-type &#8211; content-type header returned in the response
    </li>
    <li>
      mimetype &#8211; derived from the content-type response header
    </li>
    <li>
      location &#8211; the final url of the resource following any redirects
    </li>
    <li>
      content length
    </li>
    <li>
      response headers &#8211; list of all the header attribute names return in the response (just to see what other interesting stuff might be there)
    </li>
  </ul>
  
  <div id="attachment_148" style="width: 287px" class="wp-caption aligncenter">
    <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks_linktype.png"><img class="size-full wp-image-148 " title="gridworks_linktype" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks_linktype.png" alt="" width="277" height="143" /></a>
    
    <p class="wp-caption-text">
      Still to be determined how many of the url links point to some kind of data
    </p>
  </div>
  
  <div id="attachment_149" style="width: 284px" class="wp-caption aligncenter">
    <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks_parenttag.png"><img class="size-full wp-image-149" title="gridworks_parenttag" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks_parenttag.png" alt="" width="274" height="260" /></a>
    
    <p class="wp-caption-text">
      Knowing the container could help parsing out something about the semantics of the link
    </p>
  </div>
  
  <p style="text-align: center;">
    <div id="attachment_150" style="width: 284px" class="wp-caption aligncenter">
      <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks_status.png"><img class="size-full wp-image-150" title="gridworks_status" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks_status.png" alt="" width="274" height="370" /></a>
      
      <p class="wp-caption-text">
        ~70% 200's was more than I expected. Of course 200 doesn't mean it actually found something interesting.
      </p>
    </div>
    
    <div id="attachment_151" style="width: 283px" class="wp-caption aligncenter">
      <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks_contenttype.png"><img class="size-full wp-image-151" title="gridworks_contenttype" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks_contenttype.png" alt="" width="273" height="473" /></a>
      
      <p class="wp-caption-text">
        would have hoped for fewer text/html
      </p>
    </div>
    
    <div id="attachment_152" style="width: 285px" class="wp-caption aligncenter">
      <a href="http://blog.reallywow.com/static/uploads/2010/05/gridworks_domain.png"><img class="size-full wp-image-152  " title="gridworks_domain" src="http://blog.reallywow.com/static/uploads/2010/05/gridworks_domain.png" alt="" width="275" height="321" /></a>
      
      <p class="wp-caption-text">
        All the gcn.gsfc.nasa.gov hits look like observation reports, like this one, which I think is a good thing
      </p>
    </div>
    
    <p style="text-align: left;">
      Finally a thanks to <a href="http://dysinterested.com/">Sean Hannan</a> who worked out <a href="http://gist.github.com/414927">a hack</a> to a bit of the Gridworks javascript that automatically turns any cell values beginning with &#8220;http://&#8221; or &#8220;https://&#8221; into active links. The nice thing about that was it let me turn the column containing the MongoDB id into a link to a little <a href="http://webpy.org">web.py</a> script that dumps a JSON representation of the document.
    </p>
    
    <p>
      * NLM allows for links to external resources using either <a href="http://dtd.nlm.nih.gov/articleauthoring/tag-library/2.3/n-ju50.html"><ext-link></a> or <a href="http://dtd.nlm.nih.gov/articleauthoring/tag-library/2.3/n-2hw0.html"><supplementary-material></a> elements.
    </p>

 [1]: http://adsabs.harvard.edu/index.html
 [2]: http://lucene.apache.org/solr/
 [3]: http://cdsware.cern.ch/invenio/index.html
 [4]: http://iopscience.iop.org/0004-637X
 [5]: http://iopscience.iop.org/1538-3881/
 [6]: http://iopscience.iop.org/2041-8205/
 [7]: http://iopscience.iop.org/0067-0049/
 [8]: http://dtd.nlm.nih.gov/articleauthoring/
 [9]: http://code.google.com/p/freebase-gridworks/
 [10]: http://vo.ads.harvard.edu/dv/
 [11]: http://vo.ads.harvard.edu/dv/DataVerifier.cgi
 [12]: http://cda.harvard.edu/chaser/searchOcat.do?instrument=HRC-I,HRC-S,ACIS-I,ACIS-S&grating=NONE,LETG,HETG&status=observed,archived&type=TOO,CAL,GO,GTO,DDT&obsidRangeList=927&radius=10&resolver=simbad-ned&inputCoordFrame=J2000&inputCoordEquinox=2000&outputCoordFrame=J2000&outputCoordEquinox=2000&outputCoordUnits=sexagesimal&sortColumn=seqNum&sortOrder=ascending
 [13]: http://iopscience.iop.org/0004-637X/659/1/98/
 [14]: http://iopscience.iop.org/0004-637X/659/1/98/datafile2.txt
 [15]: http://iopscience.iop.org/0004-637X/661/2/845/
 [16]: http://iopscience.iop.org/0004-637X/661/2/845/70421.figures.html
 [17]: http://www.mongodb.org/
 [18]: http://vimeo.com/groups/gridworks