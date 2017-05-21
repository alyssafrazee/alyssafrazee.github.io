---
layout: post
title:  "Exploring the data on gender and GitHub repo ownership"
date:   2014-06-04
---


### an interesting graph
For several popular programming languages, this chart shows the gender breakdown of the owners of public GitHub repositories. Each owner's gender was [algorithmically predicted](https://pypi.python.org/pypi/SexMachine/) from the first name they choose to display on their GitHub profile. (Click it to see a larger static version).

<p align="center">
  <a href='bargraph.png'><img src="{{site.url}}/static/images/bargraph.png" alt="Image"/></a>
</p>

[The interactive version is here!](http://alyssafrazee.com/plgender.html) You can sort by any gender category by clicking on the corresponding box in the legend.

### a short back story
I've read a lot of internet things lately about data and women in programming/STEM. Google released its [diversity stats](http://www.google.com/diversity/at-google.html#tab=tech) last week: 17% of its technical employees are female. Last year, [this piece came out](https://medium.com/grace-hopper-2013/where-are-the-numbers-cb997a57252) seeking ([and finding](https://github.com/triketora/women-in-software-eng)) data on how many women work in the industry. And then I saw [this tweet](https://twitter.com/gdequeiroz/statuses/449677189277945856) from Gabriela de Quieroz, asking for numbers on the gender breakdown of R programmers specifically. This really caught my attention: I wonder whether the gender breakdown differs for programmers of different languages? "There _has_ to be data for that," I thought to myself (I think that thought a lot). And then I remembered that GitHub has an API...and GitHub users can identify themselves with a first name, and first names are often gendered. DATA! 

Collecting data on GitHub repository owners seemed like a fun project for several reasons:

* it could answer the language-specific gender breakdown question
* it would give some insight about who's writing open-source code -- a slightly different question than "who's currently working as a software engineer in industry?"
* it involved the entire data analysis pipeline (data collection, processing, analysis, and visualization) and would give me a chance to learn a bunch of new things!

So I went ahead with the project! I collected the data in mid-April, and I finished most of the project during [Hacker School](https://www.hackerschool.com/) reunion week in May, which was a five-day collaborative programming retreat for Hacker School alums. There, my friend [Alex](https://twitter.com/alexandrinaNYC) and I worked together to make the interactive bar chart with D3. Major thanks to her for a whole bunch of JavaScript help.

So let's get down to brass tacks: 

### the data and code
I used [GitHub's API](https://developer.github.com/v3/) and the [PyGithub](http://jacquev6.github.io/PyGithub/v1/index.html) Python wrapper for said API to collect data on all public, non-fork GitHub repositories created between May 30, 2010 and April 18, 2014, with at least 5 stars (as of 4/18/14). For each of these repos, I recorded the repo name, the repo owner's name (if provided), the repo's main programming language, the stargazer count, and the creation date. I didn't collect data on repositories owned by organizations. [Here's the code I used](https://github.com/alyssafrazee/github_analysis/blob/master/get_github_info_byday.py). Fair warning: this code takes a long time (about 60 hours) to run. [Rate limiting](https://developer.github.com/v3/#rate-limiting), what a drag. I ended up with a dataset of 168,235 repositories in total.

In an attempt to infer gender from first name, I used the Python package [SexMachine](https://pypi.python.org/pypi/SexMachine/), which classifies first names as "male", "mostly male", "neutral", "mostly female", or "female" based on how they have historically been used. Any name that isn't recognized by the classifier, including `None` (the value I recorded if a repo owner chose not to make their name public), is assigned to the "neutral" category. 

After I collected the data, I cleaned it with a [small shell script](https://github.com/alyssafrazee/github_analysis/blob/master/merge_files.sh) and [dumped it into a SQL database](https://github.com/alyssafrazee/github_analysis/blob/master/make_database.R), because I wanted to develop mad SQL query skillz. I played around with Pandas and Matplotlib and got the data ready for D3 using [this Python code](https://github.com/alyssafrazee/github_analysis/blob/master/analyze_data.py). The JavaScript/D3 code for the graph is [here](https://github.com/alyssafrazee/github_analysis/blob/master/bargraph.js).

### the results
The graph at the beginning of the post tells most of the story. The main things I noticed were:

* A pretty small percentage of starred GitHub repositories are owned by women
* There isn't a whole lot of difference in gender breakdown between languages
* There are a lot of repositories owned by users who don't provide a first name or whose first name is gender-neutral.
 
The second point gets at my original question the best: I think the data shows that the gender breakdown across languages is pretty similar. Though the different programming languages showed some variation in the absolute percentages of owners with male, female, and neutral names, the _relative_ gender distribution was pretty consistent across languages. No language showed a pattern deviating from: majority of starred repositories owned by users with male names, a good number of starred repos owned by users with neutral names, and a very small minority of repos owned by users with female names. 

Some specifics: R had the highest percent of >=5star repos with female owners (5.5%!), while Erlang had the lowest, at 0.6%. Erlang also had the highest percent of >=5star repos with male owners (74.6%), while C++ had the lowest (55.6%). The owners of Clojure repos are most likely to have identifiably gendered names: only 14% of >=5star Clojure repos have owners with neutral names. (Compare that to C++, where 38% of the owners have neutral names). 

When I showed this graphic to people, they were often surprised that R had the highest percentage of female-owned repositories. Most of them hypothesized it was because of a sample size issue. It's not: there are 452 R repositories in this dataset. (You can get a sense of each language's presence in the dataset with the  [interactive graphic](http://alyssafrazee.com/plgender.html) by clicking on the "Raw Repo Counts" checkbox on the right, which changes the y-axis to "number of repositories" instead of "percentage of repositories"). No, the real reason R wins the female percentage game is that Hadley Wickham's first name is misclassified as female, and he owns 18 highly-starred R repositories. Misclassifying the name "Hadley" in a study of R programmers' genders is a pretty unfortunate and impactful error. The story speaks to how important it is to follow up on the details of interesting analysis results. To quickly investigate this issure further, I looked at the female-classified Clojure repositories, since Clojure had the second-highest percent of female-owned repos (2.6%...) and guessed that around 12 of those 48 repositories aren't actually owned by females. In contrast, I found zero obviously misclassified male-owned R repositories. So my preliminary look into the misclassification problem suggests that it might actually be making the female percentages look _higher_ than they really are :/ To be more certain, I'd like some data on SexMachine and whether it's more prone to misclassify in one direction (i.e. misclassify more male names as female names, or vice versa). 

### so what?
The main message I took away is that a _surprisingly_ small percentage of starred GitHub repositories are owned by women. A priori, I expected maybe 20% of these repositories to have female owners. That expectation was a hunch / guesstimate / feeling. It wasn't based on any data, and I imagine it was highly influenced by my (female) vantage point. That said, available data suggests that probably more than 5% of the code out there today is written by women: [preliminary data](https://github.com/triketora/women-in-software-eng) estimates that [12.3% of software engineers are women](http://qz.com/143967/the-tech-industrys-woman-problem-statistics-show-its-worse-than-you-think/), [Google's number is 17%](http://www.google.com/diversity/at-google.html#tab=tech), and [just under 20% of B.A.s in CS were awarded to women in 2010](http://economix.blogs.nytimes.com/2013/11/15/women-gain-in-some-stem-fields-but-not-computer-science/). So what's happening with this data? Why are such a small percentage of these repositories identified as having female owners? I have several unresearched explanations:  

* Really only ~5% of the somewhat-starred repositories on GitHub are written by women
* Lots of the authors falling in the "neutral" category identify as women. (I'd say this is pretty likely. But even unreasonably assuming that _all_ the neutral classifications are women still leaves us with a majority-male-authored set of repositories).
* Women are using gender-neutral or male names on their public profiles on purpose to avoid harassment or exclusivity ([there's research on this](http://bura.brunel.ac.uk/bitstream/2438/7110/2/main-6pages.pdf); thanks [Kelsey](https://twitter.com/kelseyinnis) for pointing me toward this)
* Women aren't publicizing their code by putting it on GitHub at the same rate men are
* Repositories with female authors get starred at lower frequencies
* There were misclassification issues with the algorithm used to predict gender (though this would only skew results if misclassifications in one direction, i.e., incorrectly labeling female names as male, were more common than misclassifications in the other direction)
* ??? (I'm sure there are more theories to be researched)

I'm in the process of investigating the star issue with another dataset: last week I collected a large random sample of _all_ public GitHub repositories (regardless of fork status or stargazer count). I'm also interested in seeing if the gender patterns have changed at all over time. Analysis coming soon!

### the bigger picture
Most of the starred repositories on GitHub are owned by men, regardless of language.

I'd like this to change. I want more folks identifying as women to write code and put it up on GitHub and have it out there being used by other people. There are so, so many reasons I want to see this:

* [As said by the Ada Initiative](http://adainitiative.org/faq/#why-focus-on-women-in-open-technology-and-culture): Open technology is a powerful social force. I want women to be a visible part of that force. 
* [As said by Kelsey Gilmore-Innis](https://twitter.com/kelseyinnis/status/459703243237371907): Jobs in programming pay well, and I think it's important to broaden the base of economic power in terms of gender and race and a whole lot of other things. While a programming job is a few steps beyond putting code up on GitHub, writing and publicizing code is definitely a part of developing a tech career.
* [Inspired by this 2/21/14 post](http://plastic-idolatry.com/erik/log.html): I value radical inclusivity, and I want it in science and technology. I think diversity encourages radical inclusivity while monocultures (along almost any dimension) discourage it. 

Digging into the data on who is doing programming was fun, and I learned a lot. But I wish the results had been different.