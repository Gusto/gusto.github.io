---
permalink: /v1/considerations/versioning
layout: sidebar
title: Versioning Considerations
---

# Versioning

## Building for the Future
Versions are essentially snapshots of a given resource. If things change, we want you to find out immediately. We'd rather an extra HTTP request or 2 than employees receiving incorrect pay.

### API Layer

The Gusto API itself is versioned directly in the url - `/:version_string` - to allow for backwards compatibility. We guarantee that an application built with v1 of the API will always work, without changes, as long as that API version is supported. If we would like to implement breaking changes into the API, like changing request or response signatures, we will create a separate version of the API for new applications while supporting existing applications using our previous version.

In essence, this means changes will only be additive. A given version of the API will always provide as much or more information than when you first implement the integration.

### Object Layer

#### Idempotency

Requests are [idempotent](http://en.wikipedia.org/wiki/Idempotence#Computer_science_meaning) such that 50 identical requests will only update the data once. This applies both to retrieving information (via GET requests) as well as updating information in the Gusto ecosystem (via POST requests.)

In practice, this allows you to try identical requests multiple times without fear that data will be altered multiple times. This also means that any updates will overwrite the existing data, instead of allowing additive or incremental changes.

Idempotency is wonderful for ensuring request safety, but in order for updates to be idempotent, they must overwrite the existing data. But what if the data in Gusto has changed since you last requested it? Can you end up overwriting changes made by the other applications or the user?

#### Example

For example, let's say you wish to give Frank (with id 7) a $200 bonus for the current pay period. Unbeknownst to you, another application has already given Frank a $150 bonus. You make a request to the 'Update Payroll' endpoint with a bonus of "200.00".

Your request overwrites any bonus ($150) already in our system for employee 7 for the Feb 1 - 15 pay period.

Frank is now scheduled to receive a bonus of $200, which is $150 less than the combined value of the individual bonuses. While this may be good news for Accounting, it is obviously unacceptable.

This is why versioning extends to the object level. Objects returned from the Gusto API include a `version` field that denotes which version of the object you hold. This version is calculated based on all updatable attributes of this and child objects.

When updating an object, you must include this `version` field because it tells us how recently you have pulled information. If the data has changed since the last time you made a request, we will respond with the HTTP status code 409 Conflict. The client should request an updated version of the resource - which will include an updated `version` - and make a request with the updated information.

**Note**: Since versions are only updated when attributes that are updatable change (as opposed to any data returned by the API), they should not be relied on to monitor any change in the Gusto database. Their design is centered around preventing race conditions and overwriting data that the request couldn't have known has changed.
