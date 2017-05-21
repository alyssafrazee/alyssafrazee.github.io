---
layout: page
title : faq
permalink: /faq/
---

<h4>1. Stripe seems awesome! Are you hiring?</h4>
<p>Yes! Stripe is a great place to work and we are approximately always hiring. You can apply online at <a href="https://stripe.com/jobs">stripe.com/jobs</a>. If your background is like mine (if you love some combination of data science and software engineering), you might be particularly interested in the <a href="https://stripe.com/jobs/positions/machine-learning-engineer">Machine Learning Engineer</a> position (that's the job I have) or the <a href="https://stripe.com/jobs/positions/data-scientist">Data Scientist</a> position.</p>

<h4>2. Recurse Center seems awesome! Can you tell me more about it?</h4>
<p>The <a href="https://www.recurse.com/">Recurse Center</a> in NYC was one of the best experiences I've ever had. If you think you might like it, I'm probably going to highly encourage you to <a href="https://www.recurse.com/apply">apply</a>. If you'd like to know more details, I wrote a few blog posts while I was there about what I worked on (<a href="{{site.url}}/2013/06/02/hacker-school.html">first one</a>, <a href="{{site.url}}/2013/06/19/hacker-school-day-11.html">second one</a>, <a href="{{site.url}}/2013/08/13/sublime-plugin.html">third one</a>). I also really like my friend Julia's <a href="https://jvns.ca/blog/2014/02/15/how-was-hacker-school/">post on her time there</a>.</p>

<h4>3. I've found a bug in one of your open-source software packages!</h4>
<p>Please file an issue on the Github repo! The other maintainers and I watch the repositories and will get back to you ASAP. We also welcome pull requests :) </p>

<h4>4. I have a question about using one of your open-source software packages!</h4>
<p>You're probably going to get the best support and advice on how to use the packages from other people who are also using the software for their research. The packages people ask about are generally Bioconductor packages, and the best place to get help is support.bioconductor.org. The other maintainers and I also watch the tags for our packages, so we may also get back to you if we have time!</p>

<p>The most common open-source question I get is about our software package "ballgown" and is some variant of: <i>I have a dataset of two samples, one control and one treatment. How can I do differential expression analysis? Ballgown gives me an error.</i> To answer it publicly in an easy-to-link-to place: it is not possible to use ballgown's stattest function when you only have one sample per condition. You cannot perform statistical inference without replicates. However, all is not lost! If you want, you can rank the genes/transcripts by fold change, for example, by calculating log2(FPKM_rep1) - log2(FPKM_rep2), and you may be able to get some useful information that way. But without replicates, you can not perform statistical inference, so you can't calculate p-values, confidence intervals, standard errors or anything like that. (Variance is undefined when you have only one item). This is true for Ballgown and any other software you might use for this problem.</p>

<h4>5. How did you decide on your career path?</h4>
Feel free to <a href="{{site.url}}/contact">email me</a> about this stuff. I'm happy to email about various aspects of my (still relatively short) career so far, including things like choosing between academia and industry after a PhD, bioinformatics as it relates to data science in general, the difference between data science / data analysis / data engineering / machine learning / software engineering, and graduate school / tech in general. Maybe one day I'll write a blog post synthesizing my thoughts, but for now they mostly live in emails.
