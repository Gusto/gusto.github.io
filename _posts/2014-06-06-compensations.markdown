---
permalink: v1/compensations
layout: resource
title: Compensations
---

# Compensations

## Get compensations for a job

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/jobs/:job_id/compensations`

**Returns**: Array of all compensations associated with this job.

#### Sample Response Body:

```javascript
  [
    {
      "id" : 1363316536327004,
      "version" : "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
      "job_id" : 1123581321345589,
      "rate" : "70.00",
      "payment_unit" : "Hour",
      "flsa_status" : "Nonexempt",
      "effective_date": "2012-12-11"
    }
  ]
```

## Get a single compensation

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/compensations/:compensation_id`

**Returns**: Single compensation object

#### Sample Response Body:

```javascript
  {
    "id" : 1363316536327004,
    "version" : "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
    "job_id" : 1123581321345589,
    "rate" : "70.00",
    "payment_unit" : "Hour",
    "flsa_status" : "Nonexempt",
    "effective_date": "2012-12-11"
  }
```

## Update a compensation

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/compensations/:compensation_id`

**Returns**: Updated compensation or errors which prevented update

#### Sample Request Body:

```javascript
  {
    "version" : "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
    "rate" : "60000.00",
    "payment_unit" : "Year",
    "flsa_status" : "Exempt"
  }
```

## Create a compensation

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/jobs/:job_id/compensations`

**Returns**: Created compensation or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "rate" : "60000.00",
    "payment_unit" : "Year",
    "flsa_status" : "Exempt",
    "effective_date" : "2014-03-15"
  }
```
