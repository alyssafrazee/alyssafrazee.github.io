Title: My first pull request (or: the silver lining of a bad OS upgrade)
Date: 2014-03-15 13:13
Slug: dangit-mavericks

This is the story of a rabbit hole I went down on Thursday night. The unexpected consequence of this long journey was that I got brave enough to submit a pull request to a popular Python project!  It was my first attempt at contributing to a large-ish open-source project, and I consider that a tiny victory.

The story begins when I received my beta invite to try out [Atom](https://atom.io/), a text editor made by GitHub. Turns out that if you're on a Mac, you need Mountain Lion or Mavericks to run Atom. I was running Lion. "No problem!" I thought. I've been meaning to upgrade for a few months. So I upgraded.

This turned out to be a [mistake](http://www.youtube.com/watch?v=eFmuO6xJ36g).

I wish I would have just waited to use the new OS until I got a new laptop, because here is a (probably-incomplete) list of things that broke when I upgraded:

* my R installation
* my TeX distribution
* the [subl utility](https://www.sublimetext.com/docs/2/osx_command_line.html)
* X11 
* [SizeUp](https://www.irradiatedsoftware.com/sizeup/)
* Command Line Tools
* distutils (a crucial component of Python package installation)

I'm working on a biostatistics dissertation, which means I was filled with rage when R, TeX, my text editor's command-line tool, my remote-data-graphics-viewer, my window manager, and my Python package installer all died at the same time. (I think there was a common issue for many of these things: Mavericks seems to have messed with `/usr/local/bin`.)

So I charged forward, fixing all the broken things! Many solutions were straightforward:

* reinstall R from [the main page](http://www.r-project.org/) (also. Can we talk about how the new version of R is called "warm puppy"? Hilarious.)
* reinstall [MacTeX](http://tug.org/mactex/) 
* [change the required system preference for SizeUp](http://hopstat.wordpress.com/2013/10/29/sizeup-and-mavericks/)
* install [XQuartz](http://xquartz.macosforge.org/landing/) to replace X11, and then "log out" and log back in to get the `$DISPLAY` environment variable to recognize XQuartz

But some of the solutions were more problematic. For example: reinstalling Command Line Tools was kind of tricky. There were many problems:  

1.  I didn't want to install the entire XCode IDE
2.  The command-line installation option failed for me (as in [this post](http://stackoverflow.com/questions/20366125/xcode-select-install-failing), and I did not already have the file the answerer referenced)
3.  You have to register as an Apple developer to access the webpage where you can click and download the tools. (I have too many internet accounts.)

But, finally, after registering as an Apple developer, I got my Command Line Tools [from here](https://developer.apple.com/downloads/index.action), so, problem solved. 

The only thing left to do was to fix distutils, and that one turned out to be a doozy.  

Part of the reason this was so hard was that it took me a very, very long time to figure out that I had a _problem_ with distutils.  The _symptom_ was that my usual Python module installation process was failing for some, but not all, packages. Whether I was using `pip install`, `easy_install`, or `python setup.py install`, installation would sometimes fail with this final message:

```
Command python setup.py egg_info failed with error code 1
```

What.

There were more logs, so I read those as well:

```
distutils.errors.DistutilsError: Setup script exited with error: command 'cc' failed with exit status 1
```

and a bit further back:
```
OS/X: confusion between 'cc' versus 'gcc' (see issue 123)

will not use '__thread' in the C code

clang: error: unknown argument: '-mno-fused-madd' [-Wunused-command-line-argument-hard-error-in-future]

clang: note: this will be a hard error (cannot be downgraded to a warning) in the future
```

I repeat: What. 

So I tried my usual approach at error diagnostics: Google that sucker!  I did some hardcore internet searching for about an hour, only to find that the overwhelming majority of the internet says that the solution to `clang` Python compilation errors is "oh yeah, you just have to install Command Line Tools!  Just run `xcode-select --install` and you'll be good to go!" WRONG. You may recall that earlier in the story, I installed the Command Line Tools. Just in case I had done it wrong, I deleted my new Command Line Tools and reinstalled.  Again, the command-line installation option failed. And again, my package installation failed, with the same error. Brick wall here.

I decided to focus a bit more on this `-mno-fused-madd` situation. I'm not really in the compiling business, so I needed some more information about this elusive compiler argument.  BUT ALAS. Googling "-mno-fused-madd" [RETURNED LITERALLY ZERO RESULTS](https://www.google.com/search?btnG=1&pws=0&q=-mno-fused-madd). WHAT. 

A brief interlude from the narrative: if Google doesn't know about something, a version of me from a few years ago would assume that it was something fundamentally unknowable.  So at this point in the story, earlier-version Alyssa would have given up and gone to sleep and stopped hacking on a fundamentally unknowable thing.  But 2014 Alyssa is a Hacker School alum.  A cool thing about Hacker School is that it widened my circle of "things I believe possible," by orders of magnitude. This problem wouldn't have been in my realm of possibility two years ago, but it was _well_ within my realm on Thursday night, _despite_ being ungoogleable.  This means I was mentally fired up about this weird bug and as a result, I couldn't sleep, so I kept hacking.  

Back to the story: since `-mno-fused-madd` was ungoogleable, I Googled the larger phrase containing this mysterious compiler flag, and found [this SO question](http://stackoverflow.com/questions/22352838/ruby-gem-install-json-fails-on-mavericks-and-xcode-5-1-unknown-argument-mul), which, despite being about a Ruby gem, led me to this [XCode 5.1 Release Page](https://developer.apple.com/library/ios/releasenotes/DeveloperTools/RN-Xcode/Introduction/Introduction.html).  From there I was able to figure out a WORKAROUND! Instead of `pip install thePythonPackage`, I was able to do:

```
ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future easy_install thePythonPackage
```

I was overjoyed for many reasons:

* THE PACKAGE GOT INSTALLED. I USED IT. :tada:
* Mavericks hadn't broken `easy_install` 
* Mavericks hadn't broken my virtualenv setup

I was sad for some reasons as well:

* `ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future` is a long thing 
* They're going to take away this workaround ANY MINUTE NOW so then I will be back to square one.

So I decided to keep looking for a more permanent solution.

By this point, I had read enough internet to know that my package install was failing because somewhere in the installation process, the package was getting compiled, and the compiler was being passed this flag (the unknowable `-mno-fused-madd`) that it didn't recognize, and that was making it angry. 

THEN I remembered two important things: (1) the package I was trying to install is open-source, and the source is on GitHub, and (2) I actually know how to read and write Python, and `setup.py` is written in Python.  These two things made me think this thought: _maybe I could modify `setup.py` and take -mno-fused-madd out of the compiler flags myself_!  

So I cloned the GitHub repo and, with bated breath, searched `setup.py` for `-mno-fused-madd`. But I came up with nothing. What?! Then I went back to GitHub, where you can run full-repo code searches, and I did one for `-mno-fused-madd` on the project repo.  NOTHING!  _Then_ I realized you can do a _full GitHub code search_, so I searched all of GitHub for `-mno-fused-madd`.

And I found it.

I found the answer.

It was in a few lines of code and comments in the setup.py file of [PyMongo](https://github.com/mongodb/mongo-python-driver). Whatever genius put those lines of code in their setup file wrote this:  
```python
# PYTHON-654 - Clang doesn't support -mno-fused-madd but the pythons Apple
# ships are built with it. This is a problem starting with Xcode 5.1
# since clang 3.4 errors out when it encounters unrecognized compiler
# flags. This hack removes -mno-fused-madd from the CFLAGS automatically
# generated by distutils for Apple provided pythons, allowing C extension
# builds to complete without error. The inspiration comes from older
# versions of distutils.sysconfig.get_config_vars.
if sys.platform == 'darwin' and 'clang' in platform.python_compiler().lower():
    from distutils.sysconfig import get_config_vars
    res = get_config_vars()
    for key in ('CFLAGS', 'PY_CFLAGS'):
        if key in res:
            flags = res[key]
            flags = re.sub('-mno-fused-madd', '', flags)
            res[key] = flags
```

After playing around with this in the REPL, so I kind of knew what was going on, I pasted this block, plus some import statements, in the `setup.py` file of my clone of the project repo, ran `python setup.py install`, and: BOOYA. PACKAGE INSTALLED. AND ALSO IT WAS USABLE. 

ALYSSA (and the internet) 1, MAVERICKS 0. You think you can best me, you crazy OS upgrade, and you think you can mess with my `/usr/local/bin` folder and my C compilers and my R installation. You are wrong.

Finally, the pull request: I put those magical PyMongo lines of code into the `setup.py` file of the project that I originally wanted to install, hoping to help others avoid all the craziness that made up my Thursday night.  Boom.  First ever pull request.  Tiny victory.

I realized this morning that there's probably a larger issue here: given the explanation of the problem, it seems as though `distutils` is not playing nicely with Xcode 5.1 (i.e. the new version of Command Line Tools), which I think means the problem is going to happen with _every package relying on distutils_.  Is this right?  I drank a bunch of coffee this morning and tried for about 15 minutes to find and read the distutils source code, but I was pretty unsuccessful at that. Another day!

P.S. Remember how this entire saga began with me upgrading to Mavericks because I wanted to use Atom? Turns out Atom doesn't have syntax highlighting for R, my most-used language. 

:weary: :joy:

---
**update, 3/16/14**: It turns out that "-mno-fused-madd" is, in fact, Googleable!  I had forgotten that the dash ("-") is Google's operator for "don't include this term in search results."  When Googling command-line flags, leave out the leading dash and you're good to go! Another option is to use duckduckgo.com, which doesn't use the dash operator in the same way. (Thanks to the awesome folks in the Hacker School IRC channel for teaching me these things!)

