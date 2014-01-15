Title: finally: my ideal text editor setup
Date: 2013-08-13 12:14
Slug: sublime-plugin

Ever since I bought a Mac two years ago, I've been dreaming of a text editor that compares to the Windows-only [Notepad++](http://notepad-plus-plus.org/).  What a delight.  My favorite thing about Notepad++ was how easy it was to run code in a REPL with a keyboard shortcut (e.g., F8 would run the current line/selection of R code on your local machine, F9 would run code in a Putty SSH session...). I searched high and low for something similar for OSX.  The best I could come up with was a rather involved [Emacs configuration](working-interactively-on-a-remote-computer.html).  It was fine, just fine.  I settled.  It worked.

But I've found/made/hacked something better. Here is [line-by-line](https://github.com/alyssafrazee/Line-by-line), a [Sublime Text 2](http://www.sublimetext.com/2) plugin for OSX that executes the current line/selection in whatever REPL is running in the Terminal, with the keystroke Command-Enter.  It's [all I ever wanted](http://www.youtube.com/watch?v=is6gtilerPk) (in a text editor).  With this plugin, I'd say Sublime is at least equivalent to, and possibly better than, Notepad++, because the keystroke isn't specific to any coding language.  It just runs whatever's highlighted in Terminal.  It also works with iTerm, if you're into that kind of thing.  It's up to you to decide what REPL is running in the Terminal - which means you have the flexibility to run things in ipython, bpython, R, any REPL in an SSH session...the possibilities are endless!

All I did was *slightly* modify Randy Lai's [Enhanced-R](https://github.com/randy3k/Enhanced-R) Sublime plugin - he's the real brains behind this operation. I mostly just removed the part where Enhanced-R specifies that it's only active in R mode.  

Please download/use/enjoy if you, like me, were searching for something like this!  

#### hey, you could just use Emacs for that!  
Of course I could. You can pretty much use Emacs to do anything and everything; [it's an operating system](http://en.wikipedia.org/wiki/Editor_war).  But I already have an OS, I just want a text editor that sends lines of code to the Terminal.  Also, I don't know very much Lisp, so properly customizing Emacs is totally possible but pretty painful.  And I don't want to have to configure my editor separately for each language of code I'm writing.  

#### hey, you could just use Vim for that!  
Please.  I'm nowhere near hardcore enough to use Vim.  

#### hey, Sublime Text 2 isn't free.
And it isn't open source either.  Huge bummer.  This doesn't change the fact that it's a beautiful piece of software.  If it helps, they offer an unlimited free trial period.  

#### will my R graphics look as awesome as if I made them using the default OSX IDE? Or [RStudio](http://www.rstudio.com/)?
Totally.  If you issue a Terminal session of R a plot command, graphics are rendered in Quartz by default.  I'm a fan of Quartz.  Also, now that you mention RStudio, that was another inspiration for this plugin: one of my favorite things about R IDEs is that you can just send the code directly from your script to the REPL with Command-Enter.  Line-by-line effectively gives you something like "*Studio".  

#### How does Line-by-line work?
The one-sentence version: Just like Enhanced-R, Line-by-line calls [Applescript](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/osascript.1.html) from Python to execute the given line of code in the front-most Terminal window.

#### How do I install a Sublime plugin?
Just stick the folder with all the plugin's files in it into `~/Library/Application Support/Sublime Text 2/Packages/`.  You can also install [Package Control](https://sublime.wbond.net/), which gives you point-and-click menu options from inside Sublime.  If you have Package Control installed, you can just do Sublime Text 2 > Preferences > Package Control > Install Packages, and click the name of the package you want.  (This works for all ST2 plugins that have been made public on the Package Control website.  Line-by-line is not there.  Yet.)  

#### How do I write a Sublime plugin?
I'm planning to write another post about this soon, because I found the documentation to be kind of scattered.  The gist of it is that you write some Python (for what you want your thing to do) and some JSON (for defining keyboard shortcuts and other menu-ish things).  Being able to write/understand little extensions like this is one of the reasons I'm glad I spent a bunch of time with Python this summer.  Anyway, stay tuned!





