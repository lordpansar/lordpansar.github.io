---
layout: post
title:  "'Could not find gem X in any of the sources'"
date:  2019-05-21 11:00:00 +0200
categories: ['Ruby', 'Jekyll']
permalink: blog/could-not-find-gem-x
---
I use [Jekyll][jekyll-site] for handling the content of this blog. Jekyll is a simple static site generator based on Ruby.
Normally it's a dream working with Jekyll. You just install a gem bundle via command line and it just works.
Simple as that.

I got a new job computer a while back, and the Jekyll install I did on that computer went really FUBAR.

When running the jekyll-serve command to run the site locally, I received error messages like this one:

{% highlight shell_session %}
$ jekyll serve
C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.16.3/lib/bundler/spec_set.rb:91:in
`block in materialize': Could not find liquid-4.0.1 in any of the sources 
(Bundler::GemNotFound) from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.16.3
/lib/bundler/spec_set.rb:85:in `map!'
{% endhighlight %}

Ok. That's weird. Liquid should've been installed with the Jekyll bundle. Let's update the Jekyll gem bundle:

{% highlight shell_session %}
$ bundle update jekyll
{% endhighlight %}

Still no luck. The error message persists. Let's try to install Liquid specifically:

{% highlight shell_session %}
$ gem install liquid
Successfully installed liquid-4.0.3
Parsing documentation for liquid-4.0.3
Done installing documentation for liquid after 0 seconds
1 gem installed
{% endhighlight %}

Ok, turns out that the gem install command installed the latest version of the gem.
Maybe that doesn't matter? Let's run jekyll-serve again:

{% highlight shell_session %}
$ jekyll serve
C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.16.3/lib/bundler/runtime.rb:313:in
`check_for_activated_spec!': You have already activated liquid 4.0.3, but your Gemfile
requires liquid 4.0.1. Prepending `bundle exec` to your command may solve this.
(Gem::LoadError) from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.16.3/lib/bundler
/runtime.rb:31:in `block in setup'
{% endhighlight %}

That didn't fly. Turns out my Jekyll project is picky about gem versions. But how do I downgrade a gem? Usually it's about
upgrading stuff, not downgrading them. After some fiddling around I did this:

{% highlight shell_session %}
$ gem uninstall liquid -v 4.0.3 //specify which version to uninstall using the -v prefix
Successfully uninstalled liquid-4.0.3
{% endhighlight %}

Then reinstall the gem with the requested version

{% highlight shell_session %}
$ gem install liquid -v 4.0.1
Successfully installed liquid-4.0.1
Parsing documentation for liquid-4.0.1
Done installing documentation for liquid after 0 seconds
1 gem installed
{% endhighlight %}

After this I kept running jekyll-serve and repeating the above process until I had adjusted the versions of all the required gems.
After that, I could run my site locally. But it didn't feel right to use outdated gems, so I tried the 'bundle update jekyll' again.

And what do you know, all the gems were updated to the latest version and I was now able to run the site locally.

Disclaimer: I'm not sure if this is the best way of solving this problem, but it solved it for me!

[jekyll-site]: https://jekyllrb.com/