---
layout: page
title : writing
permalink: /writing/
---

<h4><b>blog posts</b></h4>
<ul style="list-style-type:none">
  {% for post in site.posts %}
    <li>{{ post.date | date: "%Y-%m-%d" }} - 
        <a class="post-link-main" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ul>

<h4><b>guest appearances on other blogs</b></h4>
<ul style="list-style-type:none">
  <li>2017-02-02 - <a href="https://www.infoq.com/articles/ml-optimism">Practicing Machine Learning with Optimism</a><span style="color: #aaa">, part of an InfoQ series on machine learning</span></li>
  <li>2014-04-10 - <a href="http://simplystatistics.org/2014/04/10/the-ropensci-hackathon-ropenhack/">The rOpenSci Unconference</a> <span style="color: #aaa">, my reflections on participating in ROpenSci's first hackathon</span></li>
</ul>

<h4><b>published papers</b></h4>
<ul>
  <li><a href="https://academic.oup.com/bioinformatics/article/31/17/2778/183245/Polyester-simulating-RNA-seq-datasets-with">Polyester</a>: simulating RNA-seq datasets with differential transcript expression (<i>Bioinformatics</i>, 2015). There's also <a href="https://github.com/leekgroup/polyester_code">code</a> to reproduce results in the paper and <a href="https://github.com/alyssafrazee/polyester">software</a>.</li>
  <li><a href="http://www.nature.com/nbt/journal/v33/n3/full/nbt.3172.html">Ballgown</a> bridges the gap between transcriptome assembly and expression analysis (<i>Nature Biotechnology</i>, 2015). Again there's <a href="https://github.com/leekgroup/ballgown_code">code</a> to reproduce results in the paper and <a href="https://github.com/alyssafrazee/ballgown">software</a>. The paper itself isn't open-access, but there's a <a href="http://biorxiv.org/content/early/2014/09/05/003665">free preprint</a>.</li>
  <li><a href="http://biostatistics.oxfordjournals.org/content/15/3/413">DER Finder</a>, or more formally, "Differential expression analysis of RNA-seq data at single-base resolution" (<i>Biostatistics</i>, 2014). There's <a href="https://github.com/leekgroup/derfinder">code</a> that would reproduce the paper several years ago. We also wrote a <a href="https://academic.oup.com/nar/article/45/2/e9/2953306/Flexible-expressed-region-analysis-for-RNA-seq">new and improved version</a> of DER Finder in <i>Nucleic Acids Research</i> in 2016.</li>
  <li><a href="http://www.biomedcentral.com/1471-2105/12/449">ReCount</a>: a multi-experiment resource of analysis-ready RNA-seq gene count datasets (<i>BMC Bioinformatics</i>, 2011). An updated version is coming out in 2017 in <i>Nature Biotechnology</i>!</li>
</ul>

<h4><b>some of my favorite writing by other people</b></h4>
<ul>
  <li><a href="http://www.nytimes.com/2013/09/08/opinion/sunday/you-cant-have-it-all-but-you-can-have-cake.html">You can't have it all, but you can have cake</a>, by Delia Ephron (New York Times opinion piece, September 2013)</li>
  <li><a href="https://www.usenix.org/system/files/1311_05-08_mickens.pdf">The Night Watch</a>, by James Mickens (Usenix magazine, November 2013). I would highly recommend reading everything James Mickens has written if you're the type of person that enjoys extremely funny writing about computers.</li>
  <li><a href="https://www.bitchmedia.org/article/ask-bear-how-do-i-get-okay-being-bad-stuff">How do I get okay with being bad at stuff?</a>, by S. Bear Bergman (October 2015)</li>
  <li><a href="https://allpoetry.com/Love-After-Love">Love After Love</a>, by Derek Walcott (poem, 1986)</li>
  <li><a href="http://nymag.com/thecut/2017/04/ask-polly-now-that-were-in-our-30s-im-losing-my-friends.html">Now That We’re in Our 30s, My Friends Are Abandoning Me!</a>, by Heather Havrilesky (Ask Polly, April 2017)</li>
  <li><a href="http://garann.com/dev/2013/how-to-blog-about-code-and-give-zero-fucks/">How to blog about code and give zero fucks</a>, by Garann Means (published on her blog in September 2013)</li>
  <li><a href="http://www.nytimes.com/2011/09/18/magazine/what-if-the-secret-to-success-is-failure.html">What if the secret to success is failure?</a>, by Paul Tough (New York Times Magazine, September 2011)</li>
  <li><a href="http://thatbadadvice.tumblr.com/post/78480867248/so-my-boyfriend-asked-for-a-break-over-the">Some excellent advice</a>, by the person known only (to me, at least) as the Bad Advisor (posted on her blog in March 2014)</li>
</ul>
