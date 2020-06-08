---
layout: post
title:  "Scaffolding error 'The specified deps.json [path] does not exist.' in .NET Core"
date:  2020-06-08 07:00:00 +0200
categories: ['.NET Core']
permalink: blog/deps-json-does-not-exist
---

When scaffolding new files (e.g. controllers or views) in .NET Core projects, you sometimes get a 'The specified deps.json [path] does not exist' error.

Try one of these four solutions before you throw your computer out the window:

<h4>Solution 1: Restart Visual Studio</h4>

<h4>Solution 2: Restart your computer</h4>

<h4>Solution 3: Update Visual Studio to the latest version</h4>

In the menu, go to Help > Check for Updates. If there are updates available, follow the install wizard.

![Where to find 'Check for updates' in Visual Studio 2019]({{ "/assets/images/deps-json/checkforupdates.PNG" | absolute_url }})

<h4>Solution 4: Remove the bin and obj folders from your project folder</h4>

They will be regenerated next time you build the project.