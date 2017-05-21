---
layout: post
title:  "Working interactively on a remote computer"
date:   2012-10-25
---

In my [software/hardware setup post][], I talked a little bit about
working on a remote machine.  As promised, here are the details about
how I make interactive coding easy for me.

Let's start from the very very beginning.  Our department has a pretty
sweet set of really powerful computers ("the cluster") available for us
to use.  Because the computers are so awesome, they have to be kept in a
room that is specially cooled and maintained, and they don't have
desktops that we can sit down and interact with.  As such, you need to
use a different computer (i.e., a laptop) to remotely log in to the
cluster and either (a) start an interactive session, in which you can
type commands into the Linux shell, or open up an interactive version of
(say) R or python and type commands there, or (b) submit a batch job or
shell script to run without user interaction.

Batch jobs and scripts are pretty straightforward, so I'm not going to
yammer on about that in this post.  But working interactively is a
little trickier, mostly because it's good practice (in the name of
reproducible research, scientific integrity, and organization) to keep a
record of the commands you run to get your results.  If you get results
interactively on the remote machine, there's not a built-in way to do
this.  But never fear!  Software and shortcuts exist that allow you to
save a script on your local computer, but run each line of that script
interactively on the remote machine.  Since statisticians like me
usually do most interactive work in [R][], I'll describe here how I run
a local R script interactively on the cluster.

I'm currently a Mac user, so my main tool for this purpose
is [Aquamacs][].  This is basically a version of an [Emacs][] text
editor.  My opinion on Emacs is that it's a really powerful tool, but
requires a lot of customization to access all that power, and it has
pretty funky keyboard shortcuts.  Aquamacs allows you to use either
Emacs keyboard shortcuts OR common Mac keyboard shortcuts (e.g.,
command-Z for undo) in an Emacs session, which I find really useful.
 Aquamacs makes use of [ESS][] (Emacs Speaks Statistics) when
interacting with R.

So let's get to the point: here are the steps!

​(1)  Install Aquamacs.

​(2)  Open your local R script inside Aquamacs.

​(3)  Type **M-x shell** (M means escape key), which will basically open
up a Terminal window inside Aquamacs.  (Once you hit M-x, you won't be
typing in the R script anymore, but will see your stuff appear at the
bottom of the window).

​(4)  In the Terminal window that just opened up, log in to the remote
machine. (I'm making the assumption here that the login process to the
remote machine involves some variant of an "ssh" command in the
terminal.)

​(5)  Click **Window \> Move tab to new frame**.  The terminal window
will slide over to the other side of your computer, so you're now seeing
the R script and the prompt of the remote machine simultaneously.

​(6)  Start R on the remote machine.

​(7)  Staying in the remote-machine-R window, type **M-x ess-remote**.
 You'll then be prompted for a dialect - type **r **- the line
"options(STERM='iESS')" will have been run inside your R session.

​(8)  Move back to the local R script.  You can now run line-by-line on
the remote machine either using **control-n** to run just the current
line, or using **control-r **to run a block of highlighted lines.

This has worked pretty well for me, but I am definitely interested in
hearing others' ideas if someone knows of a more efficient way to do
this from a Mac.  I use Aquamacs almost exclusively for this, which
feels a little like using a sledgehammer for a tiny little nail, since
I'm not really harnessing all the power of Aquamacs/Emacs or using it
for any of its other intended purposes, and I haven't put a lot of time
into customizing it.  But it does get the job done, and it's definitely
better than the ol' copy-paste trick.

I'm incredibly happy with my Macbook (it's a delightfully fast,
beautiful, efficient computer), but I really really miss [Notepad++][],
the best text editor I've ever known - it's Windows-only.  Running
interactively on a PC is smoother than the Mac workflow I described
above: it basically involves (1) logging into the remote machine using
something like [PuTTY][] and opening R, (2) opening up your local R
script in Notepad++, and (3) hitting F9 to run a line or highlighted set
of lines.  So much more elegantly simple!  Something for Mac software
developers to aspire to, I suppose...

  [software/hardware setup post]: http://alyssafrazee.wordpress.com/2012/08/23/hello-world/
  [R]: http://www.r-project.org/
  [Aquamacs]: http://aquamacs.org/
  [Emacs]: http://www.gnu.org/software/emacs/
  [ESS]: http://ess.r-project.org/
  [Notepad++]: http://notepad-plus-plus.org/
  [PuTTY]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
