---
layout: post
title:  "'System.IO.FileNotFoundException: Unable to find tests' in NUnit and xUnit"
date:  2018-10-17 17:00:00 +0200
categories: ['.NET', 'Testing']
permalink: blog/no-test-available-nunit
---

If you're receiving the follow error messages while setting up xUnit or NUnit for a project:

{% highlight c# %}
System.IO.FileNotFoundException: 
Unable to find tests for C:\[my purdy path]\Tests.dll
{% endhighlight %}

and

{% highlight c# %}
No test is available in C:\[My purdy path]\NUnitDemo.csproj.
Make sure that test discoverer & executors are registered and
platform & framework version settings are appropriate and try again.
{% endhighlight %}


Besides installing the obvious nugets (NUnit for example below)...

![NUnit nugets]({{ "/assets/images/nunit/nunit-nugets.PNG" | absolute_url }})

<br>... you also need to install the Microsoft.NET.Test.Sdk as well.

![Microsoft test SDK]({{ "/assets/images/nunit/test-sdk.PNG" | absolute_url }})

Clean and build solution and run your tests. Hopefully all tests will be found and ran now!