---
layout: post
title:  "Resolving HTTP 415 error in Postman"
date:  2024-10-08 05:00:00 +0200
categories: ['Postman', 'REST', 'API']
permalink: blog/http415-error-postman
---

If you receive a HTTP 415 Unsupported Media Type response ([read more about the HTTP 415 status response code here][mozilla-link]) while using
Postman, you've probably forgotten to set the Content-Type header.

In your Postman request, click the 'Headers' tab and enter 'Content-Type' as key and your media type (most likely 'application/json') as value.

![A Postman request]({{ "/assets/images/http-415-postman/postman.PNG" | absolute_url }})

Notice that Postman has been critized for the way they handle sensitive data in their cloud services. [Read more about this topic here][postman-link].

[mozilla-link]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/415
[postman-link]: https://www.leeholmes.com/security-risks-of-postman/