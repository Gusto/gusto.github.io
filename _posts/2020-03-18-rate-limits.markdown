---
permalink: /v1/basics/rate-limits
title: Rate Limits
layout: sidebar
---

# Rate Limits

Excessive calls to the Gusto API over a short period of time are subject to rate limits. Rate limits are enforced in a 60-second **rolling window**. The window opens after your first API call and closes after 60 seconds has elapsed. A new window opens when you send your next API request.

Rate limits are scoped on an application-user pair. This means that you can make 60 calls per minute on behalf of each user that has connected your application. If you make more than 60 calls for a single user in the window, subsequent requests will return responses with the HTTP status `429: Too Many Requests` until the window closes.
