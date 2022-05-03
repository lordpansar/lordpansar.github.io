---
layout: post
title:  "Creating a pull request in GitKraken"
date:  2022-05-03 04:00:00 +0200
categories: ['Git']
permalink: blog/pull-request-gitkraken
---

Pull requests is considered more or less industry standard and best practice when using Git in your projects. When you open a pull request you're essentially
saying "Yo, look at these changes I made to the project. How do you like them?". This approach allows collaborators and coworkers to review your changes and
trying them out in an isolated environment before merging (or denying) them into the repository.

And like most things in GitKraken, creating a pull request is easy as 1-2-3! There are several ways to do it, but this is my preferred way.

For this example I've created a repo on Github and then cloned it to my machine. But egads, it seems like I accidentally introduced a bug in my last
commit! D:

After noticing this, I created a feature branch where I commited a fix for the bug. After verifying that the fix does the job, I now want to open up a
pull request to merge the feature branch into the parent branch.

![GitKraken client showing repo history]({{ "/assets/images/gitkraken-pr/introduced-bug.PNG" | absolute_url }})


<h4>Step 1</h4>

Right click the feature branch and select 'Push [feature branch name] and start a pull request'.

![GitKraken right click]({{ "/assets/images/gitkraken-pr/right-click.PNG" | absolute_url }})


<h4>Step 2</h4>

Select the remote to push/pull from and the name of your branch in the upstream service (in this case Github). You can change it if you want to, but
you're good to go with the default values.

![The set origin view in GitKraken]({{ "/assets/images/gitkraken-pr/set-origin.PNG" | absolute_url }})



<h4>Step 3</h4>

Select what repo and branch you want to take the changes from and then select what repo and branch you want to merge the changes into. Best practice is
to add a title and a description to the content of your PR. You also have the option to assign reviewers, labels etc.

![The pull review creation view in GitKraken]({{ "/assets/images/gitkraken-pr/create-pr.PNG" | absolute_url }})

When you're ready, scroll down and click 'Create Pull Request'. As you can see, you also have an option to integrate with Gitlab and Bitbucket as well.


<h4>Step 4</h4>

If you navigate to your remote repo on Github and go to the Pull Requests tab you'll find the pull request we created earlier, ready for review!

![The pull request tab in Github]({{ "/assets/images/gitkraken-pr/github.PNG" | absolute_url }})

GitKraken GUI is free and available for Windows, MacOS and Linux! [Click here to download GitKraken GUI][download-link].

[download-link]: https://www.gitkraken.com/download