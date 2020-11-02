---
permalink: v1/pay_schedules
layout: sidebar
title: Pay Schedules
---

# Pay Schedules

The pay schedule object in Gusto captures the details of when employees work and
when they should be paid. A company can have multiple pay schedules.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | The unique identifier of this pay schedule
| `frequency`                     | String            |     X     |          |         | "Twice per month", "Monthly", "Every other week", or "Every week".
| `anchor_pay_date`                 | String           |     X     |          |         | The first date that employees on this pay schedule are paid with Gusto
| `day_1`                      | Integer           |     X     |     X    |         | An integer between 1 and 31 indicating the first day of the month that employees are paid. This field is only relevant for pay schedules with the "Twice per month" and "Monthly" frequencies. It will be null for pay schedules with other frequencies.
| `day_2`                      | Integer           |     X     |     X    |         | An integer between 1 and 31 indicating the second day of the month that employees are paid. This field is the second pay date for pay schedules with the "Twice per month" frequency. It will be null for pay schedules with other frequencies.
| `name`                      | String           |     X     |     X     |         | A name describing the pay group, for example, "Hourly" when all hourly employees are assigned to it, or the name of the department if the pay schedule is for an entire department. The name of the schedule is dependent on how a company decides to group employees into pay schedules and should not be used programmatically to make any assumptions.

## Get a pay schedule

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/pay_schedules/:pay_schedule_id`

**Returns**: A pay schedule

#### Sample Response Body:

```json
{
  "id": 1,
  "frequency": "Every other week",
  "anchor_pay_date": "2018-01-12",
  "day_1": null,
  "day_2": null,
  "name": "Hourly"
}
```

## Get pay schedules for the company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/pay_schedules`

**Returns**: All pay schedules for the company

#### Sample Response Body:

```json
[
  {
    "id": 1,
    "frequency": "Twice per month",
    "anchor_pay_date": "2020-05-15",
    "day_1": 15,
    "day_2": 31,
    "name": "Engineering"
  },
  {
    "id": 2,
    "frequency": "Monthly",
    "anchor_pay_date": "2020-05-31",
    "day_1": 31,
    "day_2": null,
    "name": "Sales"
  },
  {
    "id": 3,
    "frequency": "Monthly",
    "anchor_pay_date": "2020-05-31",
    "day_1": 31,
    "day_2": null,
    "name": "Staff"
  }
]
```
