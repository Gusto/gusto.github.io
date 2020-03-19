---
permalink: /v1/basics/rate-limits
title: Rate Limits
layout: sidebar
---

# Rate Limits

(Note: Applications created prior to March 1, 2020 are exempt from any rate limiting.)

Excessive calls to the Gusto API over a short period of time are subject to rate limits, scoped to an application-user pair. What this means is that for a given application, you will be limited to 60 calls per minute for each user who has connected an integration.

Rate limits are enforced as a **rolling window**, meaning that the 60 second window begins after receipt of an initial API call, and continues until that 60 seconds has elapsed. A new window will begin after another API request is received.

Should you make more than 60 requests on behalf of a single user over the course of a minute, you will begin to receive responses with HTTP status `429: Too Many Requests` until that 60 second window has elapsed.
