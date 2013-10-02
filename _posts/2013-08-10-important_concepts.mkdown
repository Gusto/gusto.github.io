---
permalink: docs/v1/important_concepts
layout: resource
---

# Important Concepts

## Some Things For Your Consideration

> Those who understand it are wise, those who do not, wander in darkness.
>
> -Isaiah Berlin

### Security

By nature, payroll information can be sensitive. As such, we take every precaution to protect the information provided to us.

#### SSL

We strictly require all API requests to be over [SSL](http://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.0). Unencrypted HTTP requests will be rejected with a 400 response status code.

<a name="versioning" markdown="1">### Versioning</a>

### Idempotency

Requests are [idempotent](http://en.wikipedia.org/wiki/Idempotence#Computer_science_meaning) such that 50 identical requests will only update the data once. This applies both to retrieving information (via GET requests) as well as updating information in the ZenPayroll ecosystem (via POST requests.)

In practice, this allows you to try identical requests multiple times without fear that data will be altered multiple times. This also means that any updates will overwrite the existing data, instead of allowing additive or incremental changes.

### Explicit vs. Contextual Intelligent Guess

Wherever possible, we prefer to have the client to specify the context precisely rather than us make assumptions that we are talking about the same thing.

For example: internally, we can identify a pay period solely by its `end_date` - we know the frequency of pay periods and can calculate `start_date`s on the fly - yet we require the `start_date` parameter when updating a payroll. This is to ensure that we both know exactly which dates data applies to. If we only required `end_date` and a company changed its pay schedule, say from monthly to bi-weekly, you could be submitting hours worked for an entire month to a 2 week pay period.

Similarly, versioning guarantees that you have up-to-date information about the state of data. This prevents race conditions and other applications unknowingly overwriting your data.