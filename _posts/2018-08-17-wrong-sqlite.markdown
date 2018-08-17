---
layout: post
title:  "'SqliteConnection' does not contain a constructor that takes 1 arguments (CS1729) and the importance of installing the correct nuget"
date:  2018-08-17 11:35:00 +0200
categories: blog xamarin
---
While setting up a SQLite DB in a Xamarin.Forms app for the first time in a while, I stumbled upon an error that made me pull my hair.

I was following this tutorial from Microsoft: [Using SQLite.NET with Android][sqlite-tutorial]

After installing the required SQLite .NET-PCL nuget package, I went forth with setting up the DB connection (step 2 in the tutorial).

{% highlight c# %}
var db = new SQLiteConnection(dbPath);
{% endhighlight %}

While trying to do this, I noticed that the SQLiteConnection class didn't have an overload that matching the number of arguments I was trying to pass.
This made me scratch my head, since according to the tutorial and my previous experience there should be one. I recieved the following error message: 

{% highlight c# %}
'SQLiteConnection' does not contain a constructor that takes 1 arguments (CS1729)
{% endhighlight %}

After taking the following measures:

<ul>
	<li>Testing other namespaces which include SQLite</li>
	<li>Doublechecking that I had the most recent version of the SQLite.NET nuget</li>
	<li>Cleaning/building the solution</li>
	<li>Restarting Visual Studio</li>
	<li>Restarting my computer</li>
	<li>Reading the <a href="https://github.com/praeclarum/sqlite-net">source code for SQLite.NET</a> to see what constructors there were available</li>
</ul>

There was nothing much but hairpulling and screaming left. Then I decided to double check the nugets one last time. That's when I saw it:

![List of nuget packages]({{ "/assets/images/sqlite-nugets.png" | absolute_url }})

I had installed "SQLite.Net-PCL" nuget when I should have installed the lowercase "sqlite-net-pcl". To further add to the confusion from the two nugets having the same name, they also have the same name (Frank Krueger).

After installing the lowercase "sqlite-net-pcl" nuget it worked like a charm.

Conclusion: if you're experiencing the same conundrum while setting up a SQLite DB in Xamarin.Forms, double check that you're not a fool for the old SQLite nuget shuffle!

[sqlite-tutorial]: https://docs.microsoft.com/en-us/xamarin/android/data-cloud/data-access/using-sqlite-orm
[source-sqlnet]: https://github.com/praeclarum/sqlite-net