Title: fun with logic, coding, and exam committees
Date: 2013-10-21 21:59
Slug: committee-checker

#### the problem
In [my department](http://biostat.jhsph.edu/), there are basically three gigantic exams you have to pass before they will give you a PhD.  The first is a written qualifier, the second is an oral exam based on a research proposal you've put together, and the third is the dissertation defense.  For both the oral exam and the defense, you have to put together a committee of about five faculty members from around the university.  Given the insane schedules of most faculty members and the very specific requirements the school has for the composition of the committee, this is no easy task.  (It's kind of nice, however, that you get to _choose_ which people you'd like to have grilling you for hours at a time, so there's that).   

The thing I noticed last year (when I was forming my oral exam committee) is that the requirements for committee composition are well-defined.  There are a lot of them, but it would basically just involve some simple logic of the if/then/else variety to check whether a given group of faculty satisfies them.  Given this, my advisor offhandedly mentioned one day that there should just be a function to check whether your proposed committee fits the school's rules.  Automatable things should be automated; brainpower should be conserved whenever possible.

#### the solution
A full year later, I actually got around to writing a little function that takes faculty member information as input and prints out whether the proposed committee will work for either your preliminary oral exam committee or your thesis committee!

The code (available [here](https://gist.github.com/alyssafrazee/7094055)) is written in R and can be sourced directly from GitHub using the `RCurl` library:

```R
library(RCurl)
codeurl = getURL("https://gist.github.com/alyssafrazee/7094055/raw/a15265f310cdfa6e51d85002f50de10767cd5fe4/checkCommittee.R")
source(textConnection(codeurl))
```

To actually check potential committees, you just create `faculty` objects for each potential committee member, then run the `checkCommittee` function on those faculty members.  You also have to tell the function your primary department and whether you're making a preliminary oral exam committee or a thesis committee.

```R
# here are some faculty members:
jeff = faculty(name="jeff", dept="biostat", sph=TRUE, advisor=TRUE, mydept=TRUE, rank="assistant", alt=FALSE)
rafa = faculty(name="rafa", dept="biostat", sph=TRUE, advisor=FALSE, mydept=TRUE, rank="full", alt=TRUE)
anthony = faculty(name="anthony", dept="bmb", sph=TRUE, advisor=FALSE, mydept=FALSE, rank="assistant", alt=FALSE)
steven = faculty(name="steven", dept="medicine", sph=FALSE, advisor=FALSE, mydept=FALSE, rank="full", alt=FALSE, joint="biostat")
kasper = faculty(name="kasper", dept="biostat", sph=TRUE, advisor=FALSE, mydept=TRUE, rank="assistant", alt=FALSE, joint="medicine")
dan = faculty(name="dan", dept="medicine", sph=FALSE, advisor=FALSE, mydept=FALSE, rank="associate", alt=FALSE)
dani = faculty(name="dani", dept="epi", sph=TRUE, advisor=FALSE, mydept=FALSE, rank="full", alt=TRUE)
ben = faculty(name="ben", dept="CS", sph=FALSE, advisor=FALSE, mydept=FALSE, rank="assistant", alt=TRUE)

# check one possible committee:
checkCommittee(jeff, rafa, anthony, steven, kasper, dan, ben, mydept="biostat", type="prelim")

# check another possible committee:
checkCommittee(jeff, rafa, anthony, steven, kasper, dan, dani, mydept="biostat", type="prelim")
```

The basic idea is that `checkCommittee` runs lots of logical tests on the set of faculty you give it, exiting with an error if something about it isn't compliant with the school's requirements. Full documentation is available in comments at the end of the gist. 

So there you have it - automated committee checking, at least for [my school](http://www.jhsph.edu/).

#### miscellaneous thoughts
- I first wrote a draft of this function in April, which was before I went to Hacker School, which meant I didn't yet realize how much nicer this code would be in Python than it is in R.  R's user-defined classes are a huge pain to create, which is why I have that hacky `faculty` function that just returns a list instead of a proper S3 or S4 class.  I find Python classes delightful and definitely would have written one called `Faculty` for this type of thing.  Between nice classes, comprehensions, and if/else blocks that don't have braces, I think Python code for this would be much more readable.  It's on my to-do list.

- For the intensely curious, [here's a link to the rules](https://gist.github.com/alyssafrazee/7094557) governing the code I wrote.

- GIANT DISCLAIMER: this isn't officially endorsed by the school - whatever this function tells you, your committee still has to be approved by your departmental academic administrator.  There are often unwritten rules as well, which are really hard to incorporate into automated tools :) 


