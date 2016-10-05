---
permalink: v1/compensations
layout: sidebar
title: Compensations
---

# Compensations

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one
that is active. The current compensation is the one with the most recent `effective_date`.

**_Note_**

Currently, jobs are arbitrarily limited to a single compensation as multiple compensations per job are not yet available
in Gusto. The API is architected as if multiple compensations may exist, so integrations should integrate under
the same assumption. The only exception is that creating a compensation with the same `job_id` as another will fail with
a relevant error.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this compensation
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `job_id`                      | Integer           |     X     |          |         | id of the job to which this compensation belongs
| `rate`                        | String            |           |          |         | dollar amount paid per payment_unit
| `payment_unit`                | String            |           |          |         | timescale accompanying the rate. Should be one of 'Hour', 'Week', 'Month', or 'Year'
| `flsa_status`                 | String            |           |          |         | FLSA status for this compensation. Salaried ("Exempt") Employees are paid a fixed salary every pay period. Hourly ("Nonexempt") Employees are paid for the hours they work, and receive overtime pay when applicable. Owners ("Owner") are employees that own at least twenty percent of the company. More information can be found on the <a href="http://www.dol.gov/whd/overtime/fs17b_executive.pdf" target="_blank">Department of Labor's site</a>.
| `effective_date`               | String           |           |    X     |[hire_date]| the effective date for this compensation rate. For the first compensation, this defaults to the job's hire_date

## Get compensations for a job

**HTTP Method**: `GET`

**Endpoint**: `/v1/jobs/:job_id/compensations`

**Returns**: Array of all compensations associated with this job.

#### Sample Response Body:

```json
[
  {
    "id": 1363316536327004,
    "version": "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
    "job_id": 1123581321345589,
    "rate": "70.00",
    "payment_unit": "Hour",
    "flsa_status": "Nonexempt",
    "effective_date": "2012-12-11"
  }
]
```

## Get a single compensation

**HTTP Method**: `GET`

**Endpoint**: `/v1/compensations/:compensation_id`

**Returns**: Single compensation object

#### Sample Response Body:

```json
{
  "id": 1363316536327004,
  "version": "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
  "job_id": 1123581321345589,
  "rate": "70.00",
  "payment_unit": "Hour",
  "flsa_status": "Nonexempt",
  "effective_date": "2012-12-11"
}
```

## Update a compensation

**HTTP Method**: `PUT`

**Endpoint**: `/v1/compensations/:compensation_id`

**Returns**: Updated compensation or errors which prevented update

#### Sample Request Body:

```json
{
  "version": "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
  "rate": "60000.00",
  "payment_unit": "Year",
  "flsa_status": "Exempt"
}
```

## Create a compensation

**HTTP Method**: `POST`

**Endpoint**: `/v1/jobs/:job_id/compensations`

**Returns**: Created compensation or errors which prevented creation

#### Sample Request Body:

```json
{
  "rate": "60000.00",
  "payment_unit": "Year",
  "flsa_status": "Exempt",
  "effective_date": "2014-03-15"
}
```
