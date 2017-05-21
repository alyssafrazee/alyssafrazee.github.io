---
layout: post
title:  "Committee Checker 2.0"
date:   2014-02-16
---

Last fall I wrote a little script that might be useful for graduate students and faculty at my school: it checks to see whether a proposed faculty committee satisfies the university's requirements. You can read more about the project in [this post](http://alyssafrazee.com/committee-checker.html). This script is now a usable web app! [Committee Checker 2.0](https://alyssafrazee.shinyapps.io/committees/) is online. Check it out and let me know what you think. The [source is on GitHub](https://github.com/alyssafrazee/committeeChecker2).

I made this into a web app (rather than leaving it as a script) beause I wanted to learn to use [Shiny](http://www.rstudio.com/shiny/), a tool for building interactive web apps with R. Committee Checker 2.0 doesn't require any plots or data visualizations, so I'm not sure it was the ideal Shiny app, but it's up and it works and it doesn't look awful! Given that I'm a statistician, not a web programmer (and certainly not a designer), I'm really happy with the result.

Some thoughts about the building process:

* Shiny is still pretty new, so it felt like the creators and I (the user) were going on a learning adventure together. I liked that.

* I liked the documentation a lot: I was able to find answers to most of the questions I had.

* There's both an [official GitHub repo](https://github.com/rstudio/shiny) and an [unofficial GitHub repo](https://github.com/rstudio/shiny-incubator) for ideas and stuff. I think that's really cool. 

* Shiny is a little less flexible than I had hoped. Let me be clear: you can _definitely_ get flexibility with a Shiny app, but you have to write your own HTML. I didn't want to do that, so that was my limitation (not Shiny's). But I think there's a happy middle ground that hasn't yet been reached: somewhere between "all visual elements decided for you" and "write your own HTML."  For example, could there be a `color` argument to `actionButton()` so I could make my "check!" button red without writing the whole UI in HTML?

* The setup made it hard to write app code that doesn't violate the "don't repeat yourself" (DRY) principle. Each input element has a unique identifier, and I couldn't figure out a way to get those identifiers into some kind of data structure so I could loop through them. I ended up working around this by either copy/pasting code, or by using non-standard evaluation + leaky scope (on purpose) to loop through identifiers for other pieces. In other words, I _really_ need a code review: my source code for this app is not great, and it's completely possible that I missed something fundamental about how to organize the input.

* Deployment is still in development. Currently there are 3 ways to deploy Shiny apps:  
    1. share the source and have users run the app locally 
    2. host on your own Linux server
    3. deploy with [ShinyApps](http://shinyapps.io/) which is in still in alpha.    

    I chose #3, because #1 defeats a good chunk of (what I see as) the purpose of building a web app, and I don't own a Linux server. Keeping in mind that ShinyApps is in alpha, it's fantastic (just what I was looking for). My app has 502-ed a couple times and I've had to re-deploy, but other than that I have no complaints.

* Commas and parens-matching were really thorny for me while writing these scripts. The error messages didn't help much. I'm actually really impressed that ["more informative error messages" is a GitHub issue](https://github.com/rstudio/shiny/issues/216) in the shiny repo!!

* User interfaces are hard!  For any non-trivial app, there are a LOT of decisions to make. I probably need help from somebody who thinks often and intentionally about good design (like my housemate, who's getting her PhD in interaction design). For this app, I spent a lot time thinking about whether the faculty should go in rows or columns and where to put the "check!" button. 

Overall, I'm glad I learned how Shiny works, and I'd love to use it in the future. I'm not sure it was the best fit for _this_ particular project: I think it's better-suited for apps involving data and graphics. Committee Checker doesn't, so I might have been able to have nicer source code if I had made it a Flask app instead. Of course, this might not be a web-app-framework issue but a language issue: I think _R_ is better-suited than _Python_ to projects involving data and graphics, but _Python_ might have been the better choice for _this_ project. That being said, I loved how easy it was to build a web app that was simple, functional, and reasonably attractive while writing only R code. 

