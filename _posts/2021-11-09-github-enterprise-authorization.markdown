---
layout: post
title:  "Authenticate GitKraken towards Github Enterprise"
date:  2021-11-09 06:00:00 +0200
categories: ['Git', 'GitKraken']
permalink: blog/authenticate-github-enterprise
---

In order to use GitKraken to sync your local repos with a remote hosted on Github Enterprise you need to add an access token to your GitKraken installation.
This token verifies that you are allowed to interact with the repos in your organization.

<h4>Step 1</h4>

Log in to your Github Enterprise organization. Click the top right icon to open the account settings dropdown and select 'Settings'.

In the next view, click 'Developer settings' in the left hand menu. Then click 'Personal access tokens'.

![The personal access token view in Github]({{ "/assets/images/github-authentication/pat-view.PNG" | absolute_url }})

Click the 'Generate new token' button.

<h4>Step 2</h4>

Now you're going to create the access token. Although it's not required, it's a good idea to add a note on what this token is used for.
E.g. 'GitKraken'. This will make it easier to keep track of your tokens if you've generated multiple ones.

![The token generation view in Github]({{ "/assets/images/github-authentication/create-pat.PNG" | absolute_url }})

Then select expiration date. Although 'No expiration' is an option, it's considered a best practice to set an expiration date.
This way you need to shift your tokens every once in a while which is better from a security point of view.

Next you need to configure what scopes your token is authorized to access. Make sure you to only select the scopes you need for your specific use case.

Notice that you can update the tokens' note and scopes after creation, but you can not update the expiration date.

When you're feeling ready, click the 'Generate token' button in the bottom of the form. 

<h4>Step 3</h4>

Now that your token has been created, you will be prompted with this view. Make sure to copy the token string. After you leave this view or refresh your browser
you won't be able to retrieve the token string again and you will need to regenerate it.

![The view after the token has been generated]({{ "/assets/images/github-authentication/after.PNG" | absolute_url }})

Depending on your organizations configuration, you might need to configure SSO before you're able to use your token. To do this, click 'Configure SSO' and log
in to your identity provider. You can also do this at a later time.

<h4>Step 4</h4>

You're now ready to add your access token to GitKraken. Start up your GitKraken client and click the preferences button in the top right corner.

Click the 'Integrations' tab and then the 'Github Enterprise' tab.

![The Github enterprise connection view]({{ "/assets/images/github-authentication/connect-gitkraken.PNG" | absolute_url }})

Add your host domain and your token string to the corresponding field in the form. Click the 'Connect' button.

You're now ready to start using GitKraken to interact with your organization. Friendly reminder that you might need to configure your SSO settings before the token
is activated. Revisit step 3 if needed.

GitKraken Git Client is free and available for Windows, MacOS and Linux! [Click here to download GitKraken][download-link].

Happy coding!

[download-link]: https://www.gitkraken.com/download
