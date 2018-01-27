---
permalink: v1/terminations
layout: sidebar
title: Terminations
---

# Terminations

Terminations are created whenever an employee is scheduled to leave the company. The only things required are an effective date (their last day of work) and whether they should receive their wages in a one-off termination payroll or with the rest of the company.

Note that some states require employees to receive their final wages within 24 hours (unless they consent otherwise,) in which case running a one-off payroll may be the only option.

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

**Endpoint**: `/v1/employees/:employee_id/terminations`

**Returns**: All terminations for this employee

#### Sample Response Body:

```json
[
  {
    "id": 891238902131212,
    "version": "d487dd0b55dfcacdd920ccbdaeafa351",
    "active": true,
    "effective_date": "{{ site.time | date: '%Y' }}-03-10",
    "run_termination_payroll": false
  }
]
```

## Get a termination for an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/terminations/:termination_id`

**Returns**: Representation of a single termination

#### Sample Response Body:

```json
{
  "id": 891238902131212,
  "version": "d487dd0b55dfcacdd920ccbdaeafa351",
  "active": true,
  "effective_date": "{{ site.time | date: '%Y' }}-03-10",
  "run_termination_payroll": false
}
```

## Update a termination

**HTTP Method**: `PUT`

**Endpoint**: `/v1/terminations/:termination_id`

**Returns**: Updated termination or errors which prevented update

#### Sample Request Body:

```json
{
  "effective_date": "{{ site.time | date: '%Y' }}-03-11"
}
```

## Create a termination

**HTTP Method**: `POST`

**Endpoint**: `/v1/employees/:employee_id/terminations`

**Returns**: Created termination or errors which prevented creation

#### Sample Request Body:

```json
{
  "effective_date": "{{ site.time | date: '%Y' }}-06-30",
  "run_termination_payroll": true
}
```
