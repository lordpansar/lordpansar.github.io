---
layout: post
title:  "Removing diagnostic settings in Azure"
date:  2021-10-19 05:00:00 +0200
categories: ['Azure', 'Powershell']
permalink: blog/remove-diag-setting
---

The other day I was removing some diagnostic settings from a few Azure resources. I was able to remove most of them via the Azure portal,
but one just wouldn't let go. No matter how many times I tried deleting it, it still remained.

After a quick googling it turns out that I wasn't the only one who had experienced this problem. Turns out you need to fix this via a CLI.

This is my solution to fixing this issue, using Powershell. If you already haven't, make sure that you have Azure CLI installed on your machine before getting started.

<h4>Step 1</h4>

Before we do anything we need to retrieve the ID of the resource to which the diagnostic setting is applied. There are multiple ways to do this,
but the easiest one is probably to navigate to the resource in the Azure Portal. Then click "JSON View" in the top right corner of the Overview blade.

![An example of a resource ID]({{ "/assets/images/remove-diag/resource-id.PNG" | absolute_url }})

Among other things, the resource ID will now be displayed. Your resource ID will probably look a little something like above.

We will also need the ID of our Azure subscription. This can be retrieved by navigating to the subscriptions blade in the Azure portal.

And finally we need the name of the diagnostic setting we're about to remove. This can be retrieved from the "Diagnostic settings" blade in the corresponding resource.

![The diagnostic settings view in Azure]({{ "/assets/images/remove-diag/setting-name.PNG" | absolute_url }})

Save the resource ID, subscription ID and diagnostic setting name, we will need them later in the process. 

<h4>Step 2</h4>

Start Powershell and run the following command:

{% highlight powershell %}
PS C:\WINDOWS\system32> Connect-AzAccount
{% endhighlight %}

You will now be prompted to login to your organization or tenant. Log in.

<h4>Step 3</h4>

To set the context to the subscription in which we are removing the diagnostic setting, enter the following command. Replace the x with your subscription ID that we retrieved in step 1.

{% highlight powershell %}
PS C:\WINDOWS\system32> Set-AzContext -Subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
{% endhighlight %}

<h4>Step 4</h4>

To remove the diagnostic setting, run the following command. Replace MyResourceID and MyDiagnosticSetting with the corresponding data from step 1.

{% highlight powershell %}
PS C:\WINDOWS\system32> Remove-AzDiagnosticSetting -ResourceId "MyResourceID" -Name MyDiagnosticSetting
{% endhighlight %}

Now you should see something like this in your Powershell window:

{% highlight powershell %}
RequestId                            StatusCode
---------                            ----------
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx         OK
{% endhighlight %}

If all went well, the diagnostic setting shold now also be gone in the Azure portal.

[Click here to read official Microsoft docs on the Set-AzContext command][setcontext-link]


[Click here to read official Microsoft docs on the Remove-AzDiagnosticSetting command][azdiag-link]

Happy coding!

[azdiag-link]: https://docs.microsoft.com/en-us/powershell/module/az.monitor/remove-azdiagnosticsetting?view=azps-6.5.0
[setcontext-link]:https://docs.microsoft.com/en-us/powershell/module/az.accounts/Set-AzContext?view=azps-6.5.0