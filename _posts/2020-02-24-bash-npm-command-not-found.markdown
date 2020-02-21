---
layout: post
title:  "Fix '-bash: command not found' NPM error in Windows 10"
date:  2020-02-24 09:00:00 +0200
categories: ['npm', 'react']
permalink: blog/bash-command-not-found
---

I was trying to start a new React Native project the other day, when I got this error message:

{% highlight shell_session %}
$ create-react-native-app my-fancy-project
-bash: create-react-app: command not found
{% endhighlight %}

Apparently this problems stems from NPM not being able to find the files needed to perform this operation. It turns out that I didn't have a correct
path set on my machine.

<h4>Step 1: Finding your way</h4>

In order to fix this you first need to find out where you keep all your NPM stuff. One way to do this is by using the 'npm config get prefix' command in
your CLI, which will return the path to your NPM folder. It might look a little something like this:

{% highlight shell_session %}
$ npm config get prefix
C:\Users\[your name]\AppData\Roaming\npm //your file path
{% endhighlight %}

Copy the path, we're going to need it later.

<h4>Step 2: Set your path</h4>

This tutorial is specific for Windows 10. This might work the same way in older Windows versions, but I haven't tried it out. If you're running MacOS -
you're on your own. If you're running Linux, you've probably solved this problem yourself and I've no idea why you're reading this blog post.

Open File Explorer, right click "This PC" and select "Properties"

![The right click menu of This PC]({{ "/assets/images/npm-path/properties.PNG" | absolute_url }})

Click "Advanced system settings"

![Computer properties]({{ "/assets/images/npm-path/system-settings.PNG" | absolute_url }})

Go to the "Advanced" tab, click the "Environment Variables" button

![System properties window]({{ "/assets/images/npm-path/system-properties.PNG" | absolute_url }})

In the "User variables" section, double click the "Path" row.

NOTICE! Do not, I repeat, DO NOT tinker with the "System variables" section. You could really mess things up if you don't know what you're doing.

![Environment variables window]({{ "/assets/images/npm-path/env-variables.PNG" | absolute_url }})

Double click an empty row in the newly opened window and paste the path you copied earlier. Make sure to not edit or delete any of your other paths,
it could mess up other installations such as Java, Ruby, emulators, SDKs etc.

![Edit environment variables window]({{ "/assets/images/npm-path/edit-env-variables.PNG" | absolute_url }})

Press OK. Back at the "System Properties" window, click apply.

Restart your CLI. Your machine should now be able to locate your NPM folder!