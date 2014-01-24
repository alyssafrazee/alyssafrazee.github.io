Title: in search of the perfect workflow
Date: 2013-10-30 22:33
Slug: workflow

As I've spent more and more time writing code and analyzing data over the past few years, it's become increasingly obvious that developing a good, comfortable workflow is _really important_.  Having a less-than-ideal step somewhere in your workflow is one of those situations where you don't even notice you have a problem until somebody fixes it for you and you're like "wow...that just totally rocked my world." 

In that spirit, I thought I'd share some of the world-rocking software, settings, or concepts that I (or more likely, my friends) have introduced into my workflow over the past few months.

##### text editor
Having a text editor you're happy with is really important, productivity-wise.  My favorite is [Sublime Text](http://www.sublimetext.com/), because (a) it's pretty, (b) there is almost no learning curve, and (c) if you can write Python, you can write extensions for it and make it do pretty much whatever you want.  My favorite extension is [Enhanced-R](https://github.com/randy3k/Enhanced-R), which lets you run R code interactively in the Terminal from Sublime (and provides some other cool features).  I actually use [my own version](https://github.com/alyssafrazee/Line-by-line) of this plugin, which is a bit more stripped-down but lets you run code from Sublime interactively in a REPL in _any_ language.  I also like [rmate](http://pogidude.com/2013/how-to-edit-a-remote-file-over-ssh-using-sublime-text-and-rmate/), which lets me use my local Sublime build to edit files on my department's computing cluster. I wrote more about editors [a few months ago](http://alyssafrazee.com/sublime-plugin.html).

##### definitely use SizeUp
[SizeUp](http://www.irradiatedsoftware.com/sizeup/) is like...pure awesomeness.  It provides keyboard shortcuts to make the current window exactly full screen, half screen, or quarter screen, and to switch between monitors if you're in to that kind of thing.  It's super nice for, say, lining up Sublime and the Terminal while you're coding. ([Be careful](http://hopstat.wordpress.com/2013/10/29/sizeup-and-mavericks/) if you're using Mavericks.  Also, fun fact: window-resizing functionality was [built in to Windows 7](http://windows.microsoft.com/en-us/windows7/products/features/snap)).

##### type, don't click
Keyboard shortcuts, keyboard shortcuts, keyboard shortcuts.  Spending a little time immersed in hacker culture will teach you that people that spend the majority of their day coding barely use the mouse at all - it's slower and easier to make mistakes.  So I've gotten familiar with [Chrome keyboard shortcuts](https://support.google.com/chrome/answer/165450?hl=en), [Gmail keyboard shortcuts](https://support.google.com/mail/answer/6594?hl=en), and [OSX keyboard shortcuts](http://interns.barrelny.com/the-mac-keyboard-shortcuts-you-didnt-know-about/) -- they're there because they're efficient.  Use them!  You can also customize the keyboard shortcuts for most software on a Mac: [here's the how-to](http://mac.tutsplus.com/tutorials/tips-shortcuts/how-to-set-up-custom-keyboard-shortcuts-on-your-mac/)!  My favorite custom one basically just shortened the "move to next tab" keystroke sequence for Sublime, Terminal, and Chrome.  

##### speed up that keyboard
Another tiny tweak that I swear has increased my productivity by like, at least 5%: Go to System Preferences --> Keyboard, set *Key Repeat* to the fastest speed and *Delay Until Repeat* to the shortest time. It's magic.  

##### keep up with the blogosphere
[Digg Reader](digg.com/reader) has eased my grief over losing Google Reader as an RSS tool.  I don't think Digg has become as popular as (say) [Feedly](feedly.com), but I tried Feedly and didn't like it as much as Digg Reader.  This just gets back to the main message: don't get complacent in your setup; it's worth it to put in the time to find something that works for you.  So...find some blogs you like, and read them productively!

##### write
I recently consolidated my official school website and my nerd blog (which I used to host on Wordpress) into this site, and I'm so happy I did that.  For this setup, I use [Pelican](http://docs.getpelican.com/en/3.2/) to generate the site and I host on [GitHub Pages](http://pages.github.com/).  Pelican lets you write posts in [Markdown](http://daringfireball.net/projects/markdown/syntax), which is super easy to write and is more flexible than the Wordpress setup.  It's especially great if you ever want to integrate code snippets into your posts.  GitHub Pages is awesome because, well, it's free web hosting, and lots of site generators (like Pelican) have built-in support for it.  I bought alyssafrazee.com from [Namecheap](namecheap.com).  

Also, I've been asked a couple times in the past few weeks how you can justify spending time blogging during a PhD (or beyond, or when you're a full-time dev...), which is a totally reasonable question, since blogging takes up a surprising amount of time.  I think there are several good reasons: to develop your voice as a writer, to practice technical writing (ask for feedback!), to share cool stuff you've learned, to strengthen your online presence...the list goes on.  [Here's a post](http://www.garann.com/dev/2013/how-to-blog-about-code-and-give-zero-fucks/) that implores developers to blog more because other developers want to know what you (yes, YOU) think. (fair warning: contains profanity). The author makes a great point: it doesn't matter if you have a big readership or not.  Your post about how you solved that super annoying bug six months ago could be invaluable to your colleague when she has the same problem tomorrow - just send her the link.  A few of us in our department get together weekly to talk about blogging, which is really fun because we can get feedback from each other, and the discussion usually turns to technical issues that are important but not directly related to the research any of us are doing.  It's really awesome.  So to sum up: you should blog, even if you think you don't have anything to say.  I know that's not directly related to workflow, but it's been a huge positive change I've made in my working life, so I thought I'd discuss it :) 

These are little changes that have made my work easier.  Would love feedback or suggestions or stories about times where a piece of software or a workflow change made your life better.  I still haven't set up comments on this blog (they'd have to be [Disqus](http://disqus.com/)...) but feel free to [email me](http://alyssafrazee.com/pages/contact.html)!

