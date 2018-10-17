---
layout: post
title:  "'System.IO.FileNotFoundException: Unable to find tests' in NUnit"
date:  2018-10-17 17:00:00 +0200
categories: ['.NET', 'Testing']
permalink: blog/no-test-available-nunit
---
I was following a tutorial for NUnit testing frameworking, but my tests wouldn't run.

I recieved the follow error messages:

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

I browsed multiple other tutorials and skimmed through a course on [Pluralsight][pluralsight] before I found stumbled on
the fix by accident.

Besides installing the NUnit and NUnit3TestAdapter nugets...

![NUnit nugets]({{ "/assets/images/nunit/nunit-nugets.PNG" | absolute_url }})

<br>... you also need to install the Microsoft.NET.Test.Sdk as well.

![Microsoft test SDK]({{ "/assets/images/nunit/test-sdk.PNG" | absolute_url }})

Clean and build solution and run your tests. Hopefully all tests will be found and ran now!

Kind of weird that none of the tutorials I checked mentioned this? I even went through a few forums discussing these very same
error messages, and there were quite a few who devs experienced the same problem.


[pluralsight]: https://pluralsight.com