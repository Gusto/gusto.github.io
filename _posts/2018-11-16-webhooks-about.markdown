---
permalink: v1/webhooks/about
title: Webhooks
layout: sidebar
---

<h1 class="block">
    Webhooks
</h1>

Please note: the webhooks API is currently in closed beta, and only available to a limited number of integrations.
We will begin to roll it out further at some point in the future.

## About
Webhooks are a way to get notified when events happen in Gusto so that you do not need to come up with a polling
strategy for refreshing data in your app.

Webhooks trigger on certain events and send an HTTP POST payload to the URL that is registered by you for that event.
You can limit which events trigger a webhook for your registered URLs.

An **event** can be an employee being created for one of your companies, or the company itself being provisioned where
access to their events were granted to you. You can create alerts in your app for running payroll based on the pay
schedule, and update it if anything changes.

A **payload** is the body of the request that will be sent to your app when an event happens. The top-level attributes
describe the resources and provide timestamps to compare to other payloads. Every payload has an `entity_attributes`
value that is the serialized entity which matches what you would have gotten if you had used our public API to get
information on that entity. This way you do not need to query our API every time an event occurs.

## Structure

```json
{
  "event_type": "employee.created",
  "entity_type": "Employee",
  "entity_id": 1123581321345589,
  "resource_type": "Company",
  "resource_id": 7757616923531095,
  "entity_attributes": { /*...*/ },
  "partner_attributes": { /*...*/ },
  "timestamp": 1533606328
}
```

| Attribute                     | Type              | Description
| :----------                   |:-------------     |:-------------
| `event_type`                  | String            | The type of event that triggered the webhook. Takes the form "{entity_type}:{action_type}". See the "Event Types" section for details.
| `entity_type`                 | String            | The type of entity that triggered the webhook. This dictates the structure of the `entity_attributes` section, and will match the structure of the corresponding API call (for instance, an entity type of "Employee" will be structured as an [employee](/v1/employees) object).
| `entity_id`                   | Integer           | The identifier to the entity that can be used to query the traditional API.
| `resource_type`               | String            | The type of parent entity that caused you to receive the event. For instance, if you have access to a company that added an employee, their company would be the resource. Or, if you instead have permission to an accounting firm with permission to manage their company, that would be the resource.
| `resource_id`                 | Integer           | The identifier of the parent entity.
| `entity_attributes`           | Object            | The representation of the entity. Its structure matches the API exactly for the given `entity_type` (except for deprovisioned events, which will only contain an identifier).
| `partner_attributes`          | Object            | Optional, partner-specific attributes that explain how the entity relates to a partner's system. Will only ever appear on `*.provisioned` events. See the [Partner Attributes](/v1/partner_attributes) section for more information.
| `timestamp`                   | Integer           | The epoch time when the entity was updated. Webhooks are not guaranteed to be delivered in-order, so you should leverage this to ensure an older event doesn't overwrite a newer one.

## Event Types
`provisioned`: Indicates that you will begin to receive webhooks for the entity. This may occur when a user opts
themselves into your integration or when you provision them through the [Accounts API](/v1/accounts).

`deprovisioned`: Indicates that a user opted out of your integration for the entity. As  such, you will no longer receive
webhooks or have API access for the entity.

`created`: A user or the Gusto system has created a new entity.

`updated`: A user or the Gusto system has changed a value of an existing entity.

Note that not all **entity** types may trigger all **event** types:

| Entity type                   | Actions that will trigger events
| :----------                   |:-------------
| company                       | `provisioned`, `deprovisioned`, `updated`
| employee                      | `created`, `updated`
| payroll                       | `created`, `updated`
| pay_schedule                  | `created`, `updated`
| location                      | `created`, `updated`

## Registering

While we are working on adding an API endpoint and eventually a GUI for registering an endpoint with our webhooks
system, the current method is to reach out to Gusto to get your webhooks setup with us.

A webhook registration will require the following:

  - An endpoint URL that we will send events to via `HTTP POST` request
  - A list of the entities that you would like to receive event notifications for
    - Current list of supported entities
      - [Company](/v1/companies)
      - [Employee](/v1/employees)
      - [Location](/v1/locations)
      - [Pay Schedule](/v1/pay_schedules)
      - [Payroll](/v1/payrolls)

After we have setup your registration and subscribed to the desired entities, we will send you a secret token that can
be used to verify subsequent notifications sent via the webhook system.

## Verification

Each webhook notification will have a header value that includes a signature you can use to verify the notification
actually came from Gusto.

The header signature will look something like this:

```
“X-Gusto-Signature”: "687b8477b067ff52af7c72903254577534434c632b48bac2f1abff170f232f89"
```

The signature value is a hex digest of the hash-based message authentication code (HMAC-SHA256) computed from the
stringified JSON payload and the secret key.

Put more simply, all webhook requests will have a 'signature' header with a hash of the request body. You can generate the
same hash from the request body using the verification token we provide when setting up our integration. As long as that
token remains secret, any request with a valid signature will have come from us.

As an example, a rails server consuming this webhook might use the following method:

```
before_action :verify_response_origin

def verify_response_origin
  computed = OpenSSL::HMAC.hexdigest(
    OpenSSL::Digest::SHA256.new,
    GUSTO_VERIFICATION_TOKEN,
    request.raw_post
  )
  actual = request.headers['X-Gusto-Signature']

  if computed != actual
    render("You're not who you say your are.", status: :bad_request)
  end
end
```
