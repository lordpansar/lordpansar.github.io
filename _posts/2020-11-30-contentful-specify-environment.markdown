---
layout: post
title:  "HTTP 403 (Forbidden) or 500 error after creating new environment in Contentful CMS"
date:  2020-11-30 14:00:00 +0200
categories: ['CMS', 'Front end']
permalink: blog/contentful-specify-environment
---

[Contentful][contentful] has great support for working with branches (they call it environments, but we all know that they're
 actually branches), for instance allowing you to make an exact copy of your production environment and use that copy
 as a dev or sand box environment.

So you make a copy of your production environment and make changes to your app config so that you will be consuming data
from your new environment. You refresh the page and this hits you in the face:
 
![A browser window showing info about a server error]({{ "/assets/images/contentful-specify-environment/server-error.PNG" | absolute_url }})

<h4>How to fix this?</h4>

In order for you (or anybody) to access the content in your new environment, you need to explicitly allow it to be accessed
using one or more of your Contentful API keys.

To do this, make sure that you're on the master branch of the affected space. Click the top left section of the header menu.

![A list of environments in a Contentful space]({{ "/assets/images/contentful-specify-environment/environment.PNG" | absolute_url }})

In the header menu, click Settings > API Keys, then under the "Content delivery/preview tokens" tab, click the affected space.

Scroll down to the "Environments" section and see whether the check box next to your new environment is ticked.

![A list of environments in a Contentful space]({{ "/assets/images/contentful-specify-environment/environments.PNG" | absolute_url }})

If needed, tick the check box. Press the "Save" button in the top right corner. You should now be able to access your new environment! 


[contentful]: https://contentful.com