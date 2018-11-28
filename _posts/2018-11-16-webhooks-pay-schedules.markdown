---
permalink: v1/webhooks/pay_schedules
title: Pay Schedules Webhooks
layout: sidebar
---

# Pay Schedules Webhooks

## Get Pay Schedule Webhook Notifications
[Webhooks Overview](/v1/webhooks/about)

**Resource**: `Company`

**Entity**: `PaySchedule` ([API Reference](/v1/pay_schedules))


**Event Types**:

- `pay_schedule.created`

- `pay_schedule.updated`

**Note** The primary use case for this event is to get Pay Periods. There are no events for Pay Periods because they are virtual and computed every time. You can use this event to in turn query our public API endpoint for a list of Pay Periods that you need for a given date range. If the Pay Schedule does not change, then the Pay Periods can be safely assumed to remain constant.

It is not advised to try and compute the Pay Schedules on your own instead of querying our API. For a monthly pay schedule alone we have 4 different ways of computing it depending on legacy logic and different needs unique to each company. Using our public API allows for the logic to remain constant across services.

You can read more about the Pay Period endpoint in our API [here](http://docs.gusto.com/v1/pay_periods).

**Returns**: Get information about a particular pay schedule that was created or updated

```json
{
  "event_type": "pay_schedule.created",
  "resource_type": "Company",
  "resource_id": 7757616923531095,
  "entity_type": "PaySchedule",
  "entity_id": 1,
  "timestamp": 1533606328,
  "entity_attributes": {
    "id": 1,
    "frequency": "Every other week",
    "anchor_pay_date": "2018-01-12",
    "day_1": null,
    "day_2": null,
    "name": "Hourly"
  }
}
```
