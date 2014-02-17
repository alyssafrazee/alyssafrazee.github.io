Title: smells like a NAMESPACE problem
Date: 2014-01-21 23:13
Slug: namespaces

Writing R packages is fun. Some people say you should start making your R code into a package [as soon as you have two functions](https://github.com/jtleek/rpackages) (just two!!). Making a package involves:

1.  Putting your function definitions into separate files and putting those files in a folder called `R`
2.  Documenting your functions in .Rd files and putting those doc files in a folder called `man`
3.  Making `DESCRIPTION` and `NAMESPACE` files

And that's it! Awesome. Mostly. (1) is pretty easy, but (2) gets snarly if you try to do it manually (never fear! [roxygen2](http://www.rstudio.com/ide/docs/packages/documentation) is here), and (3) confused me for about a year. 

Sometimes when you are confused about `DESCRIPTION` and `NAMESPACE` files, or package development in general, people and/or Google will tell you to read [the official documentation](http://cran.r-project.org/doc/manuals/R-exts.html#Creating-R-packages). Those people are wrong, unless you're really into things I don't understand, like "F95 code", "Makevars", and "pthreads". If instead you want to know what R namespaces are/why they're important and see some illustrative examples, you should read [Hadley Wickham's page about them](http://adv-r.had.co.nz/Namespaces.html), and then you should read [this delightful post](http://obeautifulcode.com/R/How-R-Searches-And-Finds-Stuff/). If you want to know about R package development in general, you should read pretty much all of [Advanced R programming](http://adv-r.had.co.nz/), Hadley's internet book, and then check out [Jeff Leek's guide to R package development](https://github.com/jtleek/rpackages).

Sometimes, even if you've read about package development, you make mistakes in your `DESCRIPTION` and `NAMESPACE` files. These kinds of mistakes can cause some really weird problems. I have made so many of these mistakes that I'm starting to recognize them as namespace mistakes (learning FTW!). In hopes of helping other people (including future Alyssa!) avoid those mistakes, here are some of the things that I've learned might indicate namespace issues:

### symptom: R can't find my function even though I loaded my package

diagnosis: failure to export. If you want a package function to be directly callable by users, you need `export(functionName)` in the `NAMESPACE` file. If you're using roxygen2, you need a `@export` tag in the docs for `functionName`. Probably you know this if you read any introductory material about package development, but it's easy to forget, especially if you have more than a few internal functions.

### symptom: error(s) when I use my function, but not when I run its lines to debug

The following frustrating sequence of events has happened to me lots of times (including earlier this afternoon):

1.  I load my brand new package
2.  I call one of its functions
3.  There's an error
4.  I find which line in the function is throwing the error with a `traceback()` 
5.  I grab that function's source, make variables with the same name as the function arguments, and run each line of the function interactively (in the global scope) so I can look at the objects and figure out what's breaking and where
6.  but everything works TOTALLY FINE IN THE GLOBAL SCOPE

diagnosis: either (a) failure to import a dependency, but having that dependency loaded in your workspace because you've called `library()` earlier in your session, or (b) relying on the `Depends` field of the `DESCRIPTION` file to specify your package's dependencies rather than the `Imports` field. There are several helpful discussions (e.g. [this](http://stackoverflow.com/questions/8637993/better-explanation-of-when-to-use-imports-depends) and [this](http://stackoverflow.com/questions/9893791/imports-and-depends)) about the difference between `Imports` and `Depends` on StackOverflow, and I'm still like 8% confused about what that difference is, but I do know this: it's usually better to put your package's dependencies in the `Imports` field. [The first answer here](http://stackoverflow.com/questions/8637993/better-explanation-of-when-to-use-imports-depends) gives a nice explanation centering around the "search path" (i.e. the order of the scopes in which R looks for function definitions when they are called; see [this post](http://obeautifulcode.com/R/How-R-Searches-And-Finds-Stuff/) for even more details). From what I understand, using `Imports` rather than `Depends` to specify dependencies has two big benefits: (1) the order in which users load your package compared to any other packages doesn't matter, and (2) loading your package won't mess up the way functions are called from other packages. Also, we wouldn't have these problems if everyone would just use `Imports` instead of `Depends`, but no such luck because please, we are R programmers, so sometimes life is hard. There are always caveats, like the [edit to the nice SO answer](http://stackoverflow.com/questions/8637993/better-explanation-of-when-to-use-imports-depends).

Anyway, to summarize this diagnosis: your package's namespace might be missing a function from a dependency. Did you forget to import a dependency? Did you specify your dependencies with `Depends` instead of `Imports`? (stop that.)

### symptom: your friends get errors when using your package on their machines, but everything works fine for you

diagnosis: Like the last symptom, this could be caused by either a failure to import a dependency and/or relying on `Depends` instead of `Imports` in `DESCRIPTION`. Check those two things, and come back.

If there are still problems, have your friends run `sessionInfo()` and check their versions of the packages that are `loaded via a namespace (and not attached)`. Do they match the versions output in your `sessionInfo()`? (things sometimes break if people are using either super old or bleeding-edge/development versions of packages). If your package requires a certain version of a package, you can add this to the package in your `DESCRIPTION` file (e.g., `Imports: sweetPackage(>=2.5.0)`. Also make sure everyone is using the newest stable version of `R`. 

### symptom: you're fixing bugs by calling functions with the :: operator
You can force your package to use functions from a specific package (say `foo`) by using `::` -- e.g., to call `foo`'s `unlist` function, you can do `foo::unlist(x)`. However, if I'm doing this inside a function I've written because I'm getting errors otherwise, and I don't need the `::` operator when I'm operating outside my package, it's sometimes an indicator I've forgotten to put either `import(foo)` or `importFrom(foo, unlist)` in my package's `NAMESPACE`.

Did I miss anything? What are your lingering unanswered questions? One of mine: can I put a package in both `Depends` AND `Imports`? If, say, I want a correct search path AND I want said package to be available interactively?
