---
layout: post
title:  "What's new in .NET 5?"
date:  2020-09-23 10:00:00 +0200
categories: ['.NET']
permalink: blog/dotnet5-whats-new
---


September 2020 marked the release of .NET 5 RC1, with a release for first stable version in November 2020. But what is .NET 5 and why should you care?

<h4>A unified .NET</h4>

One of the goals with .NET 5 was to create one .NET platform. Fusing .NET Framework, .NET Core and Mono/Xamarin into one.
There will only be one SDK. No matter if you’re making a desktop application, a web API or a mobile application - you’ll be using the same base class libraries and common APIs.

![The .NET 5 eco system]({{ "/assets/images/dotnet5/dotnet5_platform.PNG" | absolute_url }})
*Illustration courtesy of Microsoft*

<h4>Performance improvements</h4>

-	30% socket performance improvement on Linux over .NET Core 3.1
-	19% Json serialization performance improvement over .NET core 3.1
-	300% improvement in serialization of large collections and arrays – whilst not allocating any memory doing this thanks to the new zero alloc feature
-	Significant improvements to the System.Text.Json API
-	gRPC server performance exceeds Go, C++ and Java


<h4>Other new features in .NET 5</h4>

-	Support for C# 9 and F# 5
-	Introducing the ‘record’ keyword – a C# 9 feature allowing you to easily create immutable types
-	Smaller container image sizes
-	Support for ARM64 architecture
-	Greater support for assembly trimming – allowing unused types and members to be removed and thereby reducing the size of your applications
-	Single file applications. Applications that can be compiled within themselves without any version of .NET being installed on the machine(?!)
-	Out of the box OpenAPI support for web APIs
-	HttpRepl, allowing you to test and debug your APIs via command line


<h4>What’s next?</h4>

Microsoft will now try to make their releases of .NET more cyclic. Starting with .NET 5 in November 2020, Microsoft aims to release a new version of .NET every November. Even version numbers will also have long time support. This means that the version will have guaranteed support for a minimum of 3 years after release.
If you’ve installed Visual Studio 2019 v16.8 Preview 3 on your machine, .NET 5 RC1 can be downloaded [here][download].

Happy coding!

[download]: https://dotnet.microsoft.com/download/dotnet/5.0