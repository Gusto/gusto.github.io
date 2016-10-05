---
permalink: v1/garnishments
layout: sidebar
title: Garnishments
---

# Garnishments

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee's pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this garnishment
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `employee_id`                 | Integer           |     X     |          |         | id for the employee to which this garnishment belongs
| `active`                      |  Boolean          |           |     X    | true    | whether or not this garnishment is currently active
| `amount`                      |  Float            |           |          |         | amount of the garnisment. Either a percentage or fixed dollar amount.
| `description`                 | String            |           |          |         | description of this garnishment
| `court_ordered`               | Boolean           |           |          |         | whether this garnishment was court ordered
| `times`                       | Integer           |           |     X    | null    | how many times to apply this garnisment. Optional (and will be ignored) if recurring is set to `true`
| `recurring`                   | Boolean           |           |     X    | false   | if this garnishment should recur indefinitely
| `annual_maximum`              | Float             |           |     X    | null    | maximum deduction per annum. Null indicates no annual limit
| `pay_period_maximum`          | Float             |           |     X    | null    | maximum deduction per pay period. Null indicates no annual limit
| `deduct_as_percentage`        | Boolean           |           |     X    | false   | if true, treats the `amount` as a percentage to be deducted per pay period


## Get garnishments for an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/employees/:employee_id/garnishments`

**Returns**: Array of all garnishments for this employee

#### Sample Response Body:

```json
[
  {
    "id": 1363316536327000,
    "version": "63152767c822d6b0385509b973c49dda",
    "employee_id": 8964216891236743,
    "active": true,
    "amount": "100.00",
    "description": "Child support",
    "court_ordered": true,
    "times": null,
    "recurring": true,
    "annual_maximum": "400.00",
    "pay_period_maximum": null,
    "deduct_as_percentage": false
  },
  {
    "id": 1363316538400333,
    "version": "52b7c567242cb7452e89ba2bc02cb476",
    "employee_id": 8964216891236743,
    "active": true,
    "amount": "8.00",
    "description": "Company loan to employee",
    "court_ordered": false,
    "times": 5,
    "recurring": false,
    "annual_maximum": null,
    "pay_period_maximum": "100.00",
    "deduct_as_percentage": true
  }
]
```

## Get a single garnishment

**HTTP Method**: `GET`

**Endpoint**: `/v1/garnishments/:garnishment_id`

**Returns**: Single garnishment representation

#### Sample Response Body:

```json
{
  "id": 1363316538400333,
  "version": "52b7c567242cb7452e89ba2bc02cb476",
  "employee_id": 8964216891236743,
  "active": true,
  "amount": "8.00",
  "description": "Company loan to employee",
  "court_ordered": false,
  "times": 5,
  "recurring": false,
  "annual_maximum": null,
  "pay_period_maximum": "100.00",
  "deduct_as_percentage": true
}
```

## Update a garnishment

**HTTP Method**: `PUT`

**Endpoint**: `/v1/garnishments/:garnishment_id`

**Returns**: Updated garnishment or errors which prevent update

#### Sample Request Body:

```json
{
  "version": "52b7c567242cb7452e89ba2bc02cb476",
  "active": false
}
```

## Create a garnishment

**HTTP Method**: `POST`

**Endpoint**: `/v1/employees/:employee_id/garnishments/`

**Returns**: New garnishment or errors which prevented creation

#### Sample Request Body:

```json
{
  "amount": "150.00",
  "description": "Back taxes",
  "court_ordered": true,
  "recurring": true,
  "deduct_as_percentage": false
}
```
