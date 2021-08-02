---
layout: post
title:  "Using git reset in GitKraken"
date:  2021-08-10 07:00:00 +0200
categories: ['Git', 'GitKraken']
permalink: blog/reset-in-gitkraken
---

Reset is a very neat feature in Git if you want to go back in time and make a change to one or several commits. E.g. if you find an error,
typo, bug etc that you want to edit or remove.

And in GitKraken this is of course only a few clicks away.

I have for this demo created a repo with a few commits. But only after I've made the last commit, I discover that I've accidentally
commited a bug in the script.js file! D:

![A commit history graph view in GitKraken]({{ "/assets/images/gitkraken-reset/added_bug.PNG" | absolute_url }})

The horror! But fear not, this is easily fixed.

I want to undo the last commit and go back in time to the previous commit, "Added script.js", which I know contains the last working version
of script.js.

I start out by right clicking the commit I want to reset back to:

![The right click menu in GitKraken]({{ "/assets/images/gitkraken-reset/reset_rightclick.PNG" | absolute_url }})

I am now given three options - Soft, Mixed or Hard reset. Your choice will affect the state of the changes you are resetting.
In most scenarios you are fine with selecting Soft or Mixed depending on personal preference. Hard reset is reserved for royal
screw ups. I'll explain the differences shortly.
<br>
<h4>Soft reset</h4>

After making a soft reset, notice that all commit(s) made after the commit we resetted to now are gone.

![A commit history view in GitKraken after a soft reset has been made]({{ "/assets/images/gitkraken-reset/soft_reset.PNG" | absolute_url }})

All the changed files have also been uncommited and are now staged. Script.js is now reset to it's previous version, with a pending uncommited change
that you can either continue working on or discard.

<br>
<h4>Mixed reset</h4>

A mixed reset is pretty much the same thing as a soft reset. The main difference is that the affected files now are unstaged.

![A commit history view in GitKraken after a mixed reset has been made]({{ "/assets/images/gitkraken-reset/mixed_reset.PNG" | absolute_url }})

<br>
<h4>Hard reset</h4>

A hard reset is pretty much nuking the specified repo history. This can really mess up your repo, so make sure to tread carefully
when making a hard reset.

![A commit history view in GitKraken after a hard reset has been made]({{ "/assets/images/gitkraken-reset/hard_reset.PNG" | absolute_url }})

Notice that all history after the "Added script.js" commit is now gone. Like it has never existed. The same thing goes for all the affected
changes. Everything has been discarded. No changes are staged nor unstaged.

<br>
<h4>A few final words</h4>

Resetting can be a very destructive action if used improperly. In the examples above we have only resetted a single commit.

Imagine that you are trying to make a reset to a commit 20 commits behind the last one. If go forward with this, you're probably now left with
a whole lot of uncommited and unstaged changes. And all your resetted commit structure (which files and changes were associated to each commit),
commit names etc are now lost in time and space in your repo. And if you've accidentally made a hard reset but there were some things you wanted to keep - then you're really in trouble.

You should also only make resets to local commits that have not yet been pushed to a remote repo.

GitKraken GUI is free and available for Windows, MacOS and Linux! [Click here to download GitKraken GUI][download-link].

[download-link]: https://www.gitkraken.com/download