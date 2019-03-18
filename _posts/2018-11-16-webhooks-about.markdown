---
permalink: v1/webhooks/about
title: Webhooks
layout: sidebar
---

<h1 class="block">
    Webhooks
</h1>

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

The top-level attributes are webhook specific, and an example would look something like:

```json
{
  "event_type": "employee.created",
  "resource_type": "Company",
  "resource_id": 7757616923531095,
  "entity_type": "Employee",
  "entity_id": 1123581321345589,
  "timestamp": 1533606328,
  "entity_attributes": { },
  "partner_attributes": { }
}
```

In this example, `timestamp`, `event_type`, and `entity_attributes` are all standard keys to have in a webhooks payload.
Permissions are based on a resource and its entities. The parent reference is the `resource` while the `entity` is the
reference to what actually triggered the event.

Additionally, any events of type `*.provisioned` may have a `partner_attributes` key. If Gusto has a mapping of that
entity to an entity in your application, those attributes will contain your identifier to that entity. See the 
[Partner Attributes](/v1/partner_attributes) section for more information on its contents.


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
