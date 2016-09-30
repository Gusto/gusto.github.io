---
permalink: v1/paid_time_off
layout: sidebar
title: Paid Time Off
---

# Paid Time Off

These endpoints handle paid time off for an employee. Currently only 'Vacation Hours' and 'Sick Hours' are supported.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this paid time off
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `name`                        | String            |           |          |         | the name of this paid time off type. Currently only 'Vacation Hours' and 'Sick Hours' are supported
| `accrual_unit`                | String            |     X     |          |         | the unit this PTO is accrued in. Currently only 'Hour' is supported
| `accrual_period`              | String            |     X     |          |         | how often the pto accrues. Currently only 'Year' is supported
| `accrual_rate`                | String            |           |          |         | the rate at which accrual_unit is accrued per accrual_period
| `accrual_balance`             | String            |           |    X     |    0    | how many accrual_units have been accrued
| `maximum_accrual_balance`     | String            |           |    X     | null    | the maximum accrual allowed. A null value signifies no maximum accrual
| `paid_at_termination`         | Boolean           |     X     |          |         | whether to pay out the accrual_balance to the employee upon their termaination

## Get paid time off for an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/employees/:employee_id/paid_time_off`

**Returns**: All paid time off for which an employee is eligible

#### Sample Response Body:

```javascript
  [
    {
      "id": 891238902131212,
      "version" : "d487dd0b55dfcacdd920ccbdaeafa351",
      "name" : "Vacation Hours",
      "accrual_unit" : "Hour",
      "accrual_period" : "Year",
      "accrual_rate" : "160.00",
      "accrual_balance" : "20.47",
      "maximum_accrual_balance" : null,
      "paid_at_termination" : true
    },
    {
      "id": 89123890217803,
      "version" : "9dee45a24efffc78483a02cfcfd83433",
      "name" : "Sick Hours",
      "accrual_unit" : "Hour",
      "accrual_period" : "Year",
      "accrual_rate" : "80.00",
      "accrual_balance" : "9.12",
      "maximum_accrual_balance" : "100.00",
      "paid_at_termination" : false
    }
  ]
```

## Get a particular paid time off type for an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/paid_time_off/:paid_time_off_id`

**Returns**: Representation of a single paid time off

#### Sample Response Body:

```javascript
  {
    "id": 891238902131212,
    "version" : "d487dd0b55dfcacdd920ccbdaeafa351",
    "name" : "Vacation Hours",
    "accrual_unit" : "Hour",
    "accrual_period" : "Year",
    "accrual_rate" : "160.00",
    "accrual_balance" : "20.47",
    "maximum_accrual_balance" : null,
    "paid_at_termination" : true
  }
```

## Update paid time off

**HTTP Method**: `PUT`

**Endpoint**: `/v1/paid_time_off/:paid_time_off_id`

**Returns**: Updated paid time off or errors which prevented update

#### Sample Request Body:

```javascript
  {
    "accrual_rate" : "180.00",
    "maximum_accrual_balance" : "200.00"
  }
```

## Create paid time off

**HTTP Method**: `POST`

**Endpoint**: `/v1/employees/:employee_id/paid_time_off`

**Returns**: Created paid time off or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "accrual_rate" : "180.00",
    "maximum_accrual_balance" : "200.00"
  }
```
