---
permalink: v1/paid_time_off
layout: resource
title: Paid Time Off
---

# Paid Time Off

## Get paid time off for an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/employees/:employee_id/paid_time_off`

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

**Endpoint**: `/api/v1/paid_time_off/:paid_time_off_id`

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

**Endpoint**: `/api/v1/paid_time_off/:paid_time_off_id`

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

**Endpoint**: `/api/v1/employees/:employee_id/paid_time_off`

**Returns**: Created paid time off or

#### Sample Request Body:

```javascript
  {
    "accrual_rate" : "180.00",
    "maximum_accrual_balance" : "200.00"
  }
```
