---
layout: post
title:  "Testing accessibility using Web Accessibility Checker"
date:  2030-12-31 11:30:00 +0200
categories: ['.NET', 'Design', 'UX']
permalink: blog/accessibility-web-extensions
---
How much thought are you giving accessibility when designing web UI's? And if your answer is "some, I guess?",
how do you verify it's usability?

Mads Kristersen (senior PM at Visual Studio Extensibility team) at Microsoft has a number of extensions
out on Visual Studio Marketplace. One of them being the Web Accessibility Checker [(click here for more info and download)][wac].

The Web Accessibility Checker uses Browser Link to test your site's accessibility directly in the DOM. The results
are then presented in Visual Studio's error list. The extension does controls of your site using the WCAG and section
508 standards. Don't agree with the predefined rules out of the box? They can be customized. The Web Accessibility Checker
supports ASP.NET MVC, WebForms, static web sites and ASP.NET Core projects.



[wac]: https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebAccessibilityChecker
