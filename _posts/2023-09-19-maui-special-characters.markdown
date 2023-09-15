---
layout: post
title:  "Special characters in Maui/Xamarin path"
date:  2023-09-19 05:00:00 +0200
categories: ['Xamarin', 'Maui']
permalink: blog/maui-special-characters
---

I had problems on my current Windows 10 machine when doing cross platform mobile applications developement in .NET.

Whenever I was trying to build or run an Android application in either Xamarin or Maui I got the following error message:

{% highlight powershell %}
Error file not found: C:\Users\MagnusSundstrÃ¶m\AppData\Local\Temp1sdflkjd322kjdj.tmp MyPrettyProject C:\Projects\MyPrettyProject\JAVAC 1
{% endhighlight %}

Turns out that Android (or Microsoft?) doesn't like special characters. And since my last name contains the swedish letter Ö, I was down on my luck.

<h4>How to fix this?</h4>

After reaching out in variuos Microsoft and Android forums with little to no luck, out of the blue I received an email with a solution to the problem.

In your CLI of choice (I used Windows default command prompt), run the following command:

{% highlight powershell %}
mklink /D C:\Users\{faulty username from error message} C:\Users\{username with correct spelling}
{% endhighlight %}

So for me that would be:

{% highlight powershell %}
mklink /D C:\Users\MagnusSundstrÃ¶m C:\Users\MagnusSundström}
{% endhighlight %}

![A Windows command prompt with text]({{ "/assets/images/android/cmdprompt.PNG" | absolute_url }})

We've now created a symbolic link. A symbolic link is a file system object that points to another file system object.

This solved the problem for me, and I am now able to run and build Android applications on my machine.

Mad props to Jeppe S for providing me with the above solution <3 People like you make me keep my faith in mankind!