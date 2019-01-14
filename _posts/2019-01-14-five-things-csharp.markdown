---
layout: post
title:  "5 things I did not know about C#"
date:  2019-01-14 09:00:00 +0200
categories: ['.NET', 'C#']
permalink: blog/five-things-csharp
---

I've been doing a series of tweets called "Things I did not know about C#" for a while, where I've written shortly about
features and behaviours in C#. Either ones that

- I've stumbled upon
- knew they they existed but never used
- I have not fully understood how they work under the hood

I thought I should gather the first five "lessons" in a blog post. This also gives me some more space to add context and
explanation to the examples than can be fitted into a tweet.

Some of these features doesn't really make sense and you really need to wedge in an use case where they would make
sense. But after all, these are things I did not know about C# - not necessarily useful things! 
<br><br>

<h1>#1: Passing objects of different types into the same collection</h1>

I've created an empty interface, IMyPrettyInterface. The classes TypeA and TypeB are simple POCO classes,
consisting of two properties each. Both of the classes implements IMyPrettyInterface.

Normally it wouldn't be possible to pass instances of these two classes in the same collection, since the
collection would have been forced to host only one type of object.

But by declaring a list of an interface, you can add any object that implements said interface to the collection.

{% highlight c# %}
var interfaceList = new List<IMyPrettyInterface>();

//Declare objects of the two types implementing IMyPrettyInterface
var typeA = new TypeA { MyString1 = "Lorem", MyString2 = "Ipsum" };
var typeB = new TypeB { MyInt1 = 1, MyInt2 = 100 };

//No errors when adding two different object types to the same list
interfaceList.Add(typeA);
interfaceList.Add(typeB);
{% endhighlight %}
<br>
<h1>#2: Tuples allows you to have multiple return values from a method</h1>

Having been introduced in C# 7.0, tuples is a fairly new feature to the C# language.
Tuples fills its main purpose when you want to have more than one return value from a
method, but you don't want the overhead of creating a DTO class just for
this one specific usage.

There's been other ways of solving this issue before, but with tuples you get a
really clean and easy to read solution that is also compatible with async methods.

{% highlight c# %}
var user = GetUserById(123);

Console.WriteLine($"Name: {user.name} Age: {user.age}");
[Output: "Name: John Smith Age: 25"]

public static (string name, int age) GetUserById(int id)
{
   return("John Smith", 25);
} 
{% endhighlight %}
<br>
<h1>#3: The yield keyword</h1>

The yield keyword allows you rather than returning a collection, return a promise of an collection.

Below is a small app that prints the numbers 1-5. When stepping through this code (using F11 in 
Visual Studio), you'll see that the cursor will skip the first line in the method GetNumbersYield
after the first iteration. Instead it will move on to the while, verify if the condition has 
been met or not and then return an integer if the condition has been met.

{% highlight c# %}
foreach (var number in GetNumbersYield()) 
{
   Console.WriteLine(number);
}

Console.ReadLine();

static IEnumerable GetNumbersYield()
{
   var i = 1;
            
   while(i <= 5)
   {
      yield return i++;
   }
}
{% endhighlight %}

If we instead look at the example below, we've returned a list of integers instead of using yield.
These two examples does the same thing, but in this second example we initialize a list and populate it
with the numbers 1-5. Thereafter the whole list is returned, looped through and printed. As opposed
to the yield solution, a collection must be initialized and kept in memory.

{% highlight c# %}
foreach (var number in GetNumbersList()) 
{
   Console.WriteLine(number);
}

Console.ReadLine();

static IEnumerable GetNumbersList()
{
   var list = new List<int>();

   var i = 1;

   while(i <= 5)
   {
      list.Add(i++);
   }

   return list;
}
{% endhighlight %}

The community is in a divide about about this one, but in my environment (without using fancy performance
analyzers) the yield approach is about 50% faster than the "classic" approach when I've done some testing 
for comparison.
<br>
<h1>#4: The dynamic keyword</h1>

Dynamic typed variables in C#?! Isn't static typing one of the main benefits of using C#?
But before you bring out your garlic, crufixes and wooden stakes, read this through:

{% highlight c# %}
dynamic foo = 123;
foo = new MyFancyObject();
foo = "Hello world!"

Console.WriteLine(foo);
//Output: Hello world!
{% endhighlight %}

But wait a minute - why not use the var keyword? What is the difference? <br>
Answer: variables declared using 'var' get their data type set at compile time and doesn't allow changes to the data type held within.

{% highlight c# %}
var myVar = 123;
myVar = "Hello world!"
//Error CS0029 - Cannot implicitly convert type 'string' to 'int'
{% endhighlight %}

Just like in Javascript, dynamic allows you to assign and reassign any datatype or object to a variable. This is due to
the fact that the data type gets set at run time and not at compile time, which would be the case with static typing.

So what can you use this for? After reading up on the subject on forums and blogs, I find that the general opinion in the community
seems to be to avoid using dynamics in C# unless absolutely needed. 

By using dynamics you lose intellisense and the safety net that comes with static typing (e g your IDE pointing out conversion errors 
at compile time, when trying to assign values of incorrect data types to object properties etc).

An example displaying one downside of dynamics:

{% highlight c# %}
dynamic foo = 123; //Set foo to numeric value 123

MyMethod(foo); //Your IDE won't mark this as an error
//Run time exception - method expected a string, not an integer

public void MyMethod(string text)
{
	//Body
}
{% endhighlight %}

A scenario when dynamics could come in handy would be when you're expecting an object as return value, but you're not sure of what type
that object is going to be. You also might want to manipulate one or more of the object's properties.

{% highlight c# %}

dynamic myDynamic = GetObject();
myDynamic.Message = "All your base are belong to us";

public object GetObject()
{
	if(/*some condition*/)
	    return new TypeA();
	else
	    return new TypeB();
}

public class TypeA
{
	public string UniqueForTypeA { get; set;}
	public string Message { get; set; }
}

public class TypeB
{
	public int UniqueForTypeB { get; set; }
	public string Message { get; set; }
}


{% endhighlight %}

<br>
<h1>#5: The volatile keyword</h1>

When working multithreaded, you can help reducing concurrency issues  by using the volatile keyword. Be aware that this is not a foolproof
fix, but it can help minimizing the risk of certain issues common in multithreaded apps. It's still a very good idea to use the lock statement.

Example: your app is using two concurrent threads that accesses the same variable. Thread 1 makes a change to the variable's value and the
change is saved in thread 1's cache. But before the change is saved to main memory, thread 2 can still possibly get the outdated value of that
variable from main memory.

By making a variable volatile, you explicitly say that "never cache this value, write/read the main memory directly". The thread therefore gets
the most up-to-date value. Worth pointing out is that all writes in C# are always volatile. It is in the reads that this behaviour might occur.

{% highlight c# %}
   //To make a variable volatile, mark it as volatile before the data type is set
   public volatile int myInteger;
   public volatile bool myBool;
{% endhighlight %}

The compiler always tries to make performance optimizations where able. Using volatile makes the compiler skip these optimizations, and we get 
somewhat more predictable code.