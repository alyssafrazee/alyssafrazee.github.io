---
layout: post
title:  "Introducing R to a non-programmer in one hour"
date:   2014-01-02
---

My sister is a senior undergraduate majoring in sociology.  She just landed an awesome analyst job for next semester and was told she'll be using some R in the course of her work.  She asked me to show her the ropes during winter vacation, and of course I said yes!  What better way to while away the days of a Minnesota winter?!<sup>1</sup>

One catch: the day we planned to work, it turned out we only had an hour of overlapping free time. YIKES!

Challenge accepted. One hour to introduce R to my sociologist sister.  Here's what I did.  I didn't prepare this in advance, and I'm absolutely sure I made mistakes, glossed over key ideas, and/or harped on about something that's not important.  Feedback is absolutely welcome! (I'm genuinely interested in others' "R in an hour" ideas!)

### (1) download R and RStudio
I'm impressed that [RStudio](http://www.rstudio.com/) is both accessible/helpful for beginners and useful for experts.  Particularly for beginners: the point-and-click options are decent, and the `Workspace` panel is really useful for conceptualizing the R environment.  I didn't even bother showing my sister the default R IDE -- I had her download RStudio right away.  You still have to download [plain old R](http://www.r-project.org/) though, and when we did this, I learned that r-project.org could _really_ use a design overhaul, (a) because it's not very pretty and (b) downloading R is kind of confusing if you don't know what a "CRAN mirror" is.  

### (2) console and script
The first thing we did after getting set up was type two lines into the console:

```R
> x = 7
> x + 9
[1] 16
```

It wasn't exactly "hello world", but it illustrated some concepts like "assignment" and "variables" and "evaluation"<sup>2</sup>.

The next thing I had my sister do was save those two lines of code in an R script.  (I think it's important to teach beginners how to save code in a script right when they start using the language.)  Then I taught her how to do ` Cmd - Enter ` to execute those lines in the console. 

In the course of explaining this stuff, I learned that "console" and "script" are kind of jargon-y words, so I tried to give specific definitions for each of them.  I also had to be careful to use those exact words rather than things like "REPL" or "prompt."

### (3) comments

```R
# COMMENTS ARE SUPER IMPORTANT so we learned about them
```

### (4) graphics
Scripts and comments and consoles can get a little dry, so at this point, it was time for some fun with graphics! Here is the plot we made:
```R
x = rnorm(1000, mean = 100, sd = 3)
hist(x)
```
Teaching my sister about this code involved explaining what a "function" is (since both `rnorm` and `hist` are functions) and explaining what "function arguments" are and why you can refer to them by name but don't have to.

I also showed her how to save a graphic - it's easy in RStudio thanks to the handy dandy "Export" button in the graphics window.  

### (5) getting help
I think "getting help" is the most important concept to go over during this kind of session.  Obviously you're not going to learn everything in an hour, so what you really need are the _tools to go find that information_ when you need it on the job.  Here is the syntax I introduced:
```python
# if you know the function name, but not how to use it:
?chisq.test

# if you know what you want to do, but don't know the function name:
??chisquare
```
Given that function docs aren't terribly accessible thing to non-programmers, this might not have been the right tactic here.  I considered stressing the importance of Googling skillz (the single most useful thing I've learned in grad school), or introducing StackOverflow or R-help, but settled on explaining the official doc system.  I figured the answer to one of the most common beginner questions, "how do I do X in R?", would likely be "use the function `Y()`" -- so it's important to be able to figure out how `Y()` is used. 

I think the other most common beginner question is "I got this error message, Z.  How do I fix it?"  To address this issue, I demoed some common errors (`object not found`, `unexpected <X> constant`, etc.) and explained what they meant.

### (6) data types
Looking at help files reminded me that the docs often specify that certain function arguments must have a specific type, so we should probably discuss types.  I went over:

#### vectors
```R
# character vector
> y = c("apple", "apple", "banana", "kiwi", "bear", "strawberry", "strawberry")
> length(y)
[1] 7
# numeric vector
> numbers = rep(3, 99)
> numbers
 [1] 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
[39] 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
[77] 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3

```
#### matrices
```R
> mymatrix = matrix(c(10, 15, 3, 29), nrow = 2, byrow = TRUE)
> mymatrix
     [,1] [,2]
[1,]   10   15
[2,]    3   29
> t(mymatrix)
     [,1] [,2]
[1,]   10    3
[2,]   15   29
> solve(mymatrix)
           [,1]        [,2]
[1,]  0.1183673 -0.06122449
[2,] -0.0122449  0.04081633
> mymatrix %*% solve(mymatrix)
     [,1] [,2]
[1,]    1    0
[2,]    0    1
> chisq.test(mymatrix)
Pearson's Chi-squared test with Yates' continuity correction
data:  mymatrix
X-squared = 5.8385, df = 1, p-value = 0.01568
```
#### data frames (the mother of all R data types)
```R
# set working directory
setwd("~/Documents/R_intro")

# read in a dataset
wages = read.table("wages.csv", sep = ",", header = TRUE)
```
So we had discussed some data types with examples and learned some important stuff along the way, like how to find the number of elements in a vector, what a working directory is, and how to read in a data file.  

### (7) exploratory data analysis
Once you load in a dataset, things start to get fun.  We learned a whole bunch of stuff from this data frame, like how to do basic tabulations and calculate summary statistics, how to figure out if you have missing data, and how to fit a simple linear model.  This part was pretty fun because my sister started leading the session: instead of me saying "I'm going to show you how to do this," it was her asking "Hey, could we make a scatterplot?" or "Do you think we could put the best-fit line on that plot?"  I was really glad this happened - I hope it meant she was engaged and enjoying herself!
```R
> names(wages)
[1] "edlevel" "south"   "sex"     "workyr"  "union"   "wage"    "age"    
[8] "race"    "marital"
> class(wages$marital)
[1] "integer"
> table(wages$union)
not union member     union member 
             438               96 
> summary(wages$workyr)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    8.00   15.00   17.82   26.00   55.00 
> nrow(wages)
[1] 534
> length(which(is.na(wages$sex)))
[1] 0
> linmod = lm(workyr ~ age, data = wages)
> summary(linmod)
```
We also learned some more about graphics, like how to make _good_ histograms and how to create scatterplots with superimposed regression lines:
```R
hist(wages$wage, xlab = "hourly wage", main = "wages in our dataset", col = "purple")
plot(wages$age, wages$workyr, xlab = "age", ylab="years worked", main = "age vs. years worked")
abline(lm(wages$workyr ~ wages$age), col="red", lwd = 2)
```

### Aaaaand, time's up.
What did I miss?  What could have gone better?  The things that occurred to me afterward were:

* subsetting with ` [  `.  This is CLUTCH.  It applies to all the data types I introduced and it's super useful.  I wish I would have had time to ask my sister to make a histogram of wages for, say, only females. 

* programming-type things: loops, if statements, user-defined functions, etc.  I'm okay with leaving this stuff out -- I taught R here as a data analysis environment rather than a programming language, given my audience.

* saving `.rda` files and/or your workspace

* installing and loading packages

* other data types (e.g., lists)

* other (better?) resources/tips/tricks for getting help

### Final thoughts
Overall I had fun introducing R in an hour, and I think (hope?) my sister did too.  I sent her off with some other resources: [this](https://www.codeschool.com/courses/try-r), [this](http://www.cookbook-r.com/), and [this](http://www.datacamp.com/courses/introduction-to-r), none of which I'm terribly familiar with - but I know you need a lot more than an hourlong session from me to be able to analyze real data with R.  I think I covered most of the basics, and my sister said it was pretty helpful.  I'd love to hear how you'd approach the "R in an hour for a non-programmer" challenge!

#### footnotes
1. It's seriously cold here, even for Minnesota.  The temperature has been hovering around 0 for about a month now.  On Monday, the high is -12.  Fahrenheit.  I don't even.
2.  You may have noticed that I use ` = ` for assignment and that I have now passed that habit on to my sister.  I've thought about this, and I stand by it.  I think ` <- ` is a waste of keystrokes and I've only found it useful when I'm assigning something inside a `system.time` call.


