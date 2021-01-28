---
layout: post
title:  "Installing and targeting .NET 5"
date:  2021-01-28 15:30:00 +0200
categories: ['C#', '.NET']
permalink: blog/installing-dotnet5
---
In order to be able to target .NET 5 and use C# 9 in your projects you first need to install the .NET 5 SDK. [Click here to download the .NET 5 SDK][sdk].

<h4>1. Install and verify the SDK</h4>

Download the .NET 5 SDK and install it. Verify that it has been properly installed by running the command dotnet -v in a terminal.

{% highlight shell_session %}
$ dotnet -v

.NET SDK 5.0.[version]
{% endhighlight %}

<h4>2. Get Visual Studio up to par</h4> 

Make sure that you have Visual Studio 2019 v16.8 (or later) installed on your machine.

You can check your currently installed version by starting Visual Studio and clicking Help > About Microsoft Visual Studio.

If you're currently running an older version of Visual Studio 2019, click Help > Check for Updates and follow the install wizard
to install the most current version.

![The unfolded help menu in Visual Studio]({{ "/assets/images/csharp9/helpmenu.PNG" | absolute_url }})

Restart Visual Studio and/or your computer if needed.

<h4>3. Target your project for .NET 5</h4> 

Open up a project you want to target for .NET 5. Open the .csproj file and change the TargetFramework property to "net5.0".

![The contents of a csproj file in Visual Studio]({{ "/assets/images/csharp9/target.PNG" | absolute_url }})

Save changes. You are now ready to start using .NET 5 and C# 9 in this project!


[sdk]: https://dotnet.microsoft.com/download/dotnet-core