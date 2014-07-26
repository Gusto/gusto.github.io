---
permalink: v1/company_benefits
layout: resource
title: Company Benefits
---

# Company Benefits

Company benefits represent the benefits that a company is offering to employees. This ties together a particular <a href="/v1/benefits">Benefit</a> with the company-specific information for the offering of that benefit.

Note that company benefits, once created, can be disabled (`active=false`) only when no employees are enrolled.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this company benefit
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `benefit_id`                 | Integer            |     X     |          |         | id for the benefit to which this company benefit belongs
| `company_id`                 | Integer            |     X     |          |         | id for the company to which this company benefit belongs
| `active`                      |  Boolean          |           |     X    | true    | if true, employees may actively participate. May only be set to false if no employees are actively participating (e.g. if an Employee Benefit exists with this company_benefit_id)
| `description`                      |  String            |           |          |         | description of this benfit offering. For example, a company may offer multiple benefits with `benefit_id` 1 (for Medical Insurance.) So here they would put something more specific like "Kaiser Permanente" or "Blue Cross/ Blue Shield"
| `supports_percentage_amounts`               | Boolean           |      X     |          |         | if true, employee deductions and company contributions can be set as percentages of payroll for an individual employee. This is determined by the type of benefit, so not settable by the client.


## Get company benefits for a company

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/companies/:company_id/company_benefits`

**Returns**: Array of all company benefits for this employee

#### Sample Response Body:

```javascript
  [
    {
      "id": 1363316536327004
      "version": '98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872'
      "company_id": 1363316537128394
      "benefit_id": 1
      "active": true
      "description": "Kaiser Permanente"
      "supports_percentage_amounts": true
    }
  ]
```

## Get a single company benefit

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/company_benefits/:company_benefit_id`

**Returns**: Single company benefit representation

#### Sample Response Body:

```javascript
  {
    "id": 1363316536327004
    "version": '98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872'
    "company_id": 1363316537128394
    "benefit_id": 1
    "active": true
    "description": "Kaiser Permanente"
    "supports_percentage_amounts": true
  }
```

## Update a company benefit

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/company_benefits/:company_benefit_id`

**Returns**: Updated company benefit or errors which prevent update

#### Sample Request Body:

```javascript
  {
    "version": "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
    "active": false
  }
```

## Create a company benefit

**HTTP Method**: `POST`

**Endpoint**: `/api/v1/companies/:company_id/company_benefits`

**Returns**: New company benefit or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "benefit_id": 1
    "active": false
    "description": "Kaiser Permanente"
  }
```
