Title: my software/hardware setup
Date: 2012-08-23 20:29
Slug: software-setup

Inspired by the awesome [Hilary Parker][] and the dawn of a new academic
year, I've put together a rundown of tools I find essential in my
day-to-day as a biostatistics graduate student.  None of this was
formally taught to me - much has been recommended, learned on the fly,
or found via the "just Google it" method - but I hope to inject some
sense of coherence into the whole situation with this post.  We thought
something like this would be especially useful for incoming students or
anybody looking to change or optimize their setup.  So let's begin!

**Hardware**

My personal computer is a 15" MacBook Pro, which I got in October 2011.
 I was hesitant to make the switch over to the Mac (I had owned only PCs
before then), but I've never been happier with a laptop.  The work I do
on a daily basis is much better streamlined on the Mac.  However, either
platform works in our field, so I'll be sure to note when a piece of
software I discuss is Mac- or PC-specific.  The laptop is my main piece
of hardware (not counting our departmental computing cluster, which I'll
mention later) - the only other thing I'd mention is my 300GB external
hard drive, which I use to back up my computer with [Time Machine][].
 Backups are absolutely essential - I choose to use an external drive,
but backing things up in the cloud has become common practice.  I use
[Dropbox][] (you get 2GB for free) for backing up my most important
files and for creating shared folders.  Other common cloud storage
solutions are [Amazon S3][] and [SugarSync][].

**Software**

By far, my favorite piece of software is [R][] - every statistician's
best friend.  It rocks.  In the genomics world, most R packages are
published on [Bioconductor][].  The R GUI on the Mac is pretty awesome,
so working with R and Bioconductor locally required almost no setup for
me.

What was a bit more challenging was figuring out my R situation when
working on our departmental computing cluster - i.e., when working on a
remote machine that I've logged into from my laptop via ssh.  There are
two pieces of software I've found really useful when working remotely:
[Cyberduck][] (for file transfers) and [Aquamacs][] (for running code
interactively from my machine to the cluster - Mac-specific).  I'm not
fully convinced that Aquamacs is the best way to go for the interactive
code - in fact, the thing I miss most about having a PC is the text
editor [Notepad++][].  Notepad++ is a PC-specific editor that connects
beautifully to R (with [NppToR][] - just hit F8 to run a line in R
locally!) or to an ssh client (just hit F9 to run a line remotely!).
 However, I have a pretty good system worked out using Aquamacs and ESS
- I'll post the specifics in another post.  And, speaking of text
editors - I've come to like [TextWrangler][] (Mac-specific) quite a bit.

For typesetting anything with more than one equation in it, I (and most
of the mathematical/statistical community) use LaTeX.  I use
[TeXShop][] as my frontend and [MacTeX][] as my TeX distribution. This
setup works like a dream on my Mac - it's incredibly fast, and it took
NO customization to get the two features that are really important to
me: (1) automatic PDF refresh when you change your TeX code and (2) a
backward search feature where I can click on the PDF and be taken
directly to that point in the TeX code.  When I used a PC, I used
[TeXnicCenter][] as my frontend and [MiKTeX][] as my TeX distribution,
but I also found that I needed [Sumatra][] (an alternative to Adobe for
reading PDFs) and some extra customization to get my two required
features.

I use PowerPoint for presentations containing zero or one equation(s),
and I use Beamer (a LaTeX class) for anything with two or more
equations.  I have PowerPoint 2008, which is pretty slow on a Mac, so
I've been considering trying [Keynote][].  (Thoughts, anyone?).  I've
also tried to get the best of both the PowerPoint and Beamer worlds
([WYSIWYG][] + nice equations) by using [LaTeXiT][].  There's a
PC-equivalent called [Aurora][], which I used once for 30 days until my
free trial expired.

**Anything else?**

That's pretty much all I use on a daily basis.  I'll mention a couple
other miscellaneous things:  I'm just starting to use [github][] to
manage and share my code - git has great mechanisms for keeping track of
all the craziness that comes with doing a shared project.  Lots of
people in my department use [Sweave][], a cool way to integrate R and
LaTeX.  I am not one of those people.  Sweave is especially good for
putting together manuals, but not so good for working with analyses that
take a while to run or that need to be very specifically formatted.

I'd love to hear about any setup tips that you find useful - do share!

  [Hilary Parker]: http://hilaryparker.com/2012/08/16/the-setup-part-1/
  [Time Machine]: http://support.apple.com/kb/HT1427
  [Dropbox]: http://www.dropbox.com
  [Amazon S3]: http://aws.amazon.com/s3/
  [SugarSync]: https://www.sugarsync.com/
  [R]: http://www.r-project.org/
  [Bioconductor]: http://bioconductor.org
  [Cyberduck]: http://cyberduck.ch/
  [Aquamacs]: http://aquamacs.org/
  [Notepad++]: http://notepad-plus-plus.org/
  [NppToR]: http://sourceforge.net/projects/npptor/
  [TextWrangler]: http://www.barebones.com/products/TextWrangler/
  [TeXShop]: http://pages.uoregon.edu/koch/texshop/index.html
  [MacTeX]: http://www.tug.org/mactex/2011/
  [TeXnicCenter]: http://www.texniccenter.org/
  [MiKTeX]: http://miktex.org/
  [Sumatra]: http://blog.kowalczyk.info/software/sumatrapdf/free-pdf-reader.html
  [Keynote]: http://www.apple.com/iwork/keynote/
  [WYSIWYG]: http://en.wikipedia.org/wiki/WYSIWYG
  [LaTeXiT]: http://pierre.chachatelier.fr/latexit/latexit-home.php?lang=en
  [Aurora]: http://elevatorlady.ca/
  [github]: http://github.com
  [Sweave]: http://www.statistik.lmu.de/~leisch/Sweave/
