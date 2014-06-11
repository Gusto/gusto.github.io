---
permalink: v1/terminations
layout: resource
title: Terminations
---

# Terminations

These enpoints handle paid time off for an employee. Currently only 'Vacation Hours' and 'Sick Hours' are supported.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this termination
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions

| `employee_id`                 | Integer           |     X     |          |         | id of the employee to which this information is attached
| `active`                      | Boolean           |     X     |          |         | whether the employee's termination has gone into effect.
| `effective_date`              | String            |           |          |         | the employee's last day of work
| `run_termination_payroll`     | Boolean           |           |          |         | if true, employee will recieve their last, prorated wages via an offcycle payroll. If false, they will recieve their final wages with the rest of the company


## Get terminations for an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/employees/:employee_id/terminations`

**Returns**: All terminations for this employee

#### Sample Response Body:

```javascript
  [
    {
      "id": 891238902131212,
      "version" : "d487dd0b55dfcacdd920ccbdaeafa351",
      "active" : true,
      "effective_date" : "2014-03-10",
      "run_termination_payroll" : false
    }
  ]
```

## Get a particular paid time off type for an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/terminations/:termination_id`

**Returns**: Representation of a single termination

#### Sample Response Body:

```javascript
  {
    "id": 891238902131212,
    "version" : "d487dd0b55dfcacdd920ccbdaeafa351",
    "active" : true,
    "effective_date" : "2014-03-10",
    "run_termination_payroll" : false
  }
```

## Update a termination

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/termination/:termination_id`

**Returns**: Updated termination or errors which prevented update

#### Sample Request Body:

```javascript
  {
    "effective_date" : "2014-03-11"
  }
```

## Create paid time off

**HTTP Method**: `POST`

**Endpoint**: `/api/v1/employees/:employee_id/terminations`

**Returns**: Created termination or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "effective_date" : "2014-06-30",
    "run_termination_payroll" : true
  }
```
