---
id: 172
title: List of networks used in GeneMANIA
date: 2011-06-20T15:02:43+00:00
author: max
layout: page
guid: http://pages.genemania.org/?page_id=172
wpautop:
  - 'false'
---
[toc]

<div id="networks">
  <p>
    [php]
  </p>
  
  <p>
    function file_get_contents_utf8($fn) {<br /> $content = file_get_contents($fn);<br /> return mb_convert_encoding($content, &#8216;UTF-8&#8217;,<br /> mb_detect_encoding($content, &#8216;UTF-8, ISO-8859-1&#8217;, true));<br /> }
  </p>
  
  <p>
    echo file_get_contents_utf8(&#8220;http://genemania.org/networks&#8221;);<br /> [/php]
  </p>
</div>