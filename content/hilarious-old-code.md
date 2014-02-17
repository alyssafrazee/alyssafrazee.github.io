Title: Today I read some code I wrote in 2007 and laughed
Date: 2014-01-29 11:59
Slug: old-code

A few weeks ago, I heard or read something like this: "if you look back at work you did a while ago and you think it was really awful, _this is a good thing_ because it means you're improving." 

I remember thinking this was a great attitude to have toward old work that you now look upon with shame. Instead of getting caught up in how terrible it seems, get caught up in how far you've come since then! Positive thinking, encouragement, etc etc etc. I'm sorry I can't remember where I heard this (if it was you who said this to me, let me know and I'll give you the appropriate shout-out!).

Today I was doing a little re-organization of my hard drive when I came across some of the R code I wrote in college, when I was first learning about R and data analysis and statistics. I almost thought "oh my goodness I shouldn't put this on the internet! It's hilariously awful!" but then I thought maybe "it's hilariously awful!" was a great reason to put it on the internet: non-beginners will be entertained, and beginners might be encouraged! So, I give you: a script I wrote for my statistics class in the fall of 2007, which I had creatively and informatively titled `september12.R`:

<script src="https://gist.github.com/alyssafrazee/8702020.js"></script>

Some fun features:

- number of comments: 0
- everything is saved, even my mistakes (cf. lines 8, 19, 31)
- oh my, `attach()` is used! ("bad form" in any non-trivial data analysis project)
- the mystery of lines 25-28: This looks like some convoluted library loads that I evidently was using in order to make a dot plot...? And I'm calling `:::`?! I guarantee you I had no idea what these lines were doing and had copy/pasted them from class notes to make `DOTplot` work.
- the use of R as a calculator in lines 21-24, with no explanation of why (though it looks like I was calculating outlier cutoffs using IQR)

So many feelings. :grimacing: :joy: :flushed: :worried:

Happily, I've improved as an R programmer since 2007. I was curious as to how much R code I've written since then, so I went on a little detour and did a quick analysis of my hard drive: how many lines of R do I have stored in the following folders: `Documents`, `Google Drive`, `Dropbox`, and `Desktop`? (I wanted to exclude R code from my installed libraries and applications - I'm interested in code that _I_ have written). By this metric, I estimate that I've written **437,878** lines of R. In these folders, I also have 130,912 lines of Python (a lot of which is attributable to my Hacker School summer) and 1431 lines of C++ (from my college software design class!). 

Anyway, after writing 437K lines of R, my code is now a little nicer! Here's something I wrote last month:

<script src="https://gist.github.com/alyssafrazee/8702510.js"></script>

Some things I apparently learned between writing that first bit of code and writing this bit:

- how to name files better (this one was named `first_simulation.R`)
- how to write R packages
- how to put those R packages on GitHub
- how to write functions (kind of required for R package development)
- how to comment code
- how to create variables
- what a FASTA file is
- etc.

Also, as I looked for an example of "good" code to put in this post, I learned that in general, data analysis code is pretty ugly. There's a difference between writing _programs_ and _functions_ and writing code that _loads_, _cleans_, and _analyzes data_. Right now, I'm finding it a lot easier to write nice, clean programs and functions than to write a beautiful data analysis script. Perhaps there's also a language component (I have some _really beautiful_ Python), but I do think data analysis is kind of a messy process. 

Thanks for laughing at my code from 7 years ago with me :) 

