---
layout: post
title:  "Fun with git: making a subdirectory into a new repository"
date:   2014-05-01
---

Today I wanted to make a new GitHub repository from a subdirectory of an existing repository, preserving the commit history. There's a [nice help article](https://help.github.com/articles/splitting-a-subpath-out-into-a-new-repository) on how to do this, but I had to do a bit of exploration (read: break a few things) to learn what would happen when I followed those instructions. Here are the details on what I ended up doing! 

The goal: pop the `polyester` subdirectory of my `ballgown` repository into its own repository. 

First we will need to clone the `ballgown` repository:
```
git clone git@github.com:alyssafrazee/ballgown.git
```
I got confused for a minute and thought I should just `cd` to my existing local copy of this repository, but no! We need a _second_ local copy of the original repository.

Now let's rename the folder that was just created to the subdirectory name (i.e., what our new repo will be called), and change to that folder:

```
mv ballgown polyester
cd polyester
```

Here's where the magic happens: use the `filter-branch` command to bring the subdirectory contents (and history of non-empty commits) into this folder and onto the master branch:
```
git filter-branch --prune-empty --subdirectory-filter polyester master
```

Our current directory has just been overwritten with the contents of the subdirectory! This is a good thing. This is also why we didn't just do this in our original local copy of the `ballgown` repository. Now we just need to push this stuff into a new GitHub repo.

To do this, we'll create the new GitHub repository online. It will have the same name as the subdirectory we just popped out (`polyester`). I initialized the new repository without a `README`, `.gitignore`, or `LICENSE`, since I already had a README in my subfolder, and I wanted to avoid pulling and/or merge conflicts.

Finally, to push the contents to the new repository, we'll have to change the origin: we initially cloned from `ballgown` but now want to push to `polyester`.
```
git remote rm origin
git remote add origin git@github.com:alyssafrazee/polyester.git
git push origin master
```

The last thing I did was delete the `polyester` subdirectory from the original `ballgown` repository. And that's all! Now what used to be in the `polyester` subdirectory of my `ballgown` repo now lives in its _own_ GitHub repo, and it still has the whole commit history in it. Cool.
