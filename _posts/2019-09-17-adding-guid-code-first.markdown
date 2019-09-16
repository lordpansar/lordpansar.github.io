---
layout: post
title:  "Adding a GUID to an existing table in a EF code first migration"
date:  2019-09-17 06:00:00 +0200
categories: ['.NET', 'Entity Framework Core', 'C#']
permalink: blog/add-guid-ef-code-first
---

The other day I was trying to add a new column to an existing table using Entity Framework Core.
The column should hold a unique GUID for each row as a default value. Easier said than done.

After making my changes to my entity class, I ran the add-migration command in the package manager console.

{% highlight shell_session %}
PM> add-migration MyPurdyMigration
{% endhighlight %}

In the migration file generated, I experimented with setting the defaultValue parameter to different takes
on a new GUID object, but it ended up with EF inserting the same GUID value in all rows. Not very distinct and unique.

![A database column with identical values]({{ "/assets/images/ef-guid/not-unique-guids.PNG" | absolute_url }})

After that I tried changing defaultValue to defaultValueSql and setting it to the string value "newId()".

{% highlight c# %}
protected override void Up(MigrationBuilder migrationBuilder)
{
    migrationBuilder.AddColumn<Guid>(
    name: "UniqueId",
    table: "Orders",
    nullable: false,
    defaultValueSql: "newId()");
} 
{% endhighlight %}

After that I ran the update-database command in the PM console.

{% highlight shell_session %}
PM> update-database
{% endhighlight %}

This solved my problem and my table was populated with a new column containing unique GUIDs.

![A database column with unique values]({{ "/assets/images/ef-guid/unique-guids.PNG" | absolute_url }})