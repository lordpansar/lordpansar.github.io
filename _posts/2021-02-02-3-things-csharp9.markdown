---
layout: post
title:  "3 new features in C# 9"
date:  2021-02-02 20:00:00 +0200
categories: ['C#', '.NET']
permalink: blog/3-things-csharp9
---

.NET 5 was released in November 2020. With it came C# 9. In this article we're taking a look at a few new features of this
(at the time of publishing) latest installment of C#.

Please notice: in order to be able to use C# 9 in your projects you need to install the .NET 5 on your machine and also target your project for .NET 5 as well.
[Click here for instructions on how to install and target .NET 5][install-post].
<br><br>
<h4>Updated pattern matching</h4>

In C# 9 pattern matching has become more semantic in it's syntax, giving you the option to describe conditions and queries with words instead of symbols
(!=, ==, && etc). 

These keywords can be used wherever 'is patterns' are allowed, e.g. if statements and switch expressions.

{% highlight csharp %}

//The 'or' operator

var list = new List<string> { "apple", "banana", "orange", "lemon", "kiwi", "kumquat" };

var fruits = list.Where(fruit => fruit is "apple" or "lemon");

COMPARED TO

var fruits = list.Where(fruit => fruit == "apple" || name == "lemon");

//OUTPUT: apple, lemon

-----------------------------------------------------------------

//The 'not' operator

var fruits = list.Where(fruit => fruit is not "banana");

COMPARED TO

var fruits = list.Where(fruit => fruit != "banana");

//OUTPUT: apple, orange, lemon, kiwi, kumquat

{% endhighlight %}

{% highlight csharp %}

//The 'and' operator

var fruit = "banana";

if(fruit is not "orange" and not "apple")
{
    Console.WriteLine("This is not an orange, nor is it an apple!");
}

COMPARED TO

if(fruit != "orange" && fruit != "apple")
{
    Console.WriteLine("This is not an orange, nor is it an apple!");
}

//OUTPUT: This is not an orange, nor is it an apple!

{% endhighlight %}

Some of you might write this off as syntactic sugar. But depending on your preferences and coding style this can be used to increase 
your code's readability where applied.

<br><br>

<h4>The shortened 'new' expression</h4>

When instantiating an explicitly typed object you now have to option to use a short form of the 'new' expression.  

Let's say we have a POCO class describing a car:

{% highlight csharp %}

public class Car
{
    public string Color { get; set; }
    public int ConstructionYear { get; set; }
}

{% endhighlight %}

When creating a new instance of the class, we now have an option to create the instance as such:

{% highlight csharp %}

Car myPrettyCar = new();

COMPARED TO

Car myPrettyCar = new Car();

{% endhighlight %}

You can also directly assign values to the new object's properties as usual.

{% highlight csharp %}

Car myPrettyCar = new() { Color = "Red", ConstructionYear = 2020 };

{% endhighlight %}

And use a class constructor.

{% highlight csharp %}

public class Car
{
    public Car(string color, int year)
    {
        Color = color;
        ConstructionYear = year;
    }

    public string Color { get; set; }
    public int ConstructionYear { get; set; }
}

Car myPrettyCar = new("Yellow", 2018);

{% endhighlight %}

<br><br>

<h4>Init only setters</h4>

One of the most talked about features of C# 9 is records (which we won't go over here since it deserves a post on it's own).
Records helps .NET developers create immutable objects, which has always been somewhat of a hassle in C#. Init only setters does somewhat
the same thing.

By setting an object property's set accessor as 'init', you tell your application that this property can only be set when the object is being
instantiated.

Let's recycle our car POCO class from the previous example, but modify the construction year property with an init setter:

{% highlight csharp %}

public class Car
{
    public string Color { get; set; }
    public int ConstructionYear { get; init; }
}

{% endhighlight %}

Here we allow instances of the car class to have it's color updated, but by using the 'init' as accessor we only allow the construction year
to be assigned during initialization.

{% highlight csharp %}

Car myPrettyCar = new() { Color = "Purple", ConstructionYear = 2021 };

myPrettyCar.Color = "Blue"; //This is OK
myPrettyCar.ConstructionYear = 2005; //Compilation error!

{% endhighlight %}

By adding the init setter we've gotten another tool to our encapsulation toolbox, allowing us to make some or all of the properties of a
class immutable after instantiation. We can now expose our object properties as if they were public, yet shield them without setting them as private.


[install-post]: https://magnussundstrom.se/blog/installing-dotnet5
