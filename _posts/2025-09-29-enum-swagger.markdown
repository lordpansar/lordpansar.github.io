---
layout: post
title:  "Prettifying enum values in Swagger"
date:  2025-09-29 04:00:00 +0200
categories: ['Swagger', '.NET', "API", "OpenAPI"]
permalink: blog/prettify-swagger
---

By default, C# enums are serialized to their underlying numeric values when included in a JSON response.
This is what you’ll see not only in Swagger, but also in tools like Postman or Insomnia, since they simply display whatever your .NET API outputs.

If you want the enum name (it's string representation) to appear instead of the numeric value, you need to adjust the JSON serialization settings.

For example, let's say that we have an API endpoint that returns an instance of the User class below.

{% highlight csharp %}
public class User
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Role Role { get; set; }
}

public enum Role
{
    User = 1,
    Editor = 2,
    Admin = 3
}
{% endhighlight %}

By default Swagger will render the numeric representation of the Role property in the JSON response.

{% highlight json %}
{
  "name": "Alex",
  "age": 35,
  "role": 1
}
{% endhighlight %}

<h4>Step 1</h4>

In order to show the display name/text value of the enum, we need to add an annotation to the Role property.

{% highlight csharp %}
public class User
{
    public string Name { get; set; }
    public int Age { get; set; }
    [JsonConverter(typeof(JsonStringEnumConverter))]
    public Role Role { get; set; }
}
{% endhighlight %}

After adding the annotation, the Role property will now be rendered as it's text value.

{% highlight json %}
{
  "name": "Alex",
  "age": 35,
  "role": "User"
}
{% endhighlight %}

<h4>Step 2</h4>

After performing step 1 your enum property will be rendered as it's text value. But in your schema definition
you will still see the numeric value.

You can resolve this by making this change in your Program.cs file.

{% highlight csharp %}
builder.Services.AddControllers();

//change into =>

builder.Services.AddControllers().AddJsonOptions(options =>
    options.JsonSerializerOptions.Converters.Add(new JsonStringEnumConverter()));
{% endhighlight %}

If you're using Minimal API, add this to your Program.cs file instead:

{% highlight csharp %}

builder.Services.Configure<JsonOptions>(options => 
	{ options.JsonSerializerOptions.Converters.Add(new JsonStringEnumConverter()); });

{% endhighlight %}


Happy coding!
