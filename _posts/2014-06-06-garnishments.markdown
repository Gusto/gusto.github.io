---
permalink: v1/garnishments
layout: resource
title: Garnishments
---

# Garnishments

## Get garnishments for an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/employees/:employee_id/garnishments`

**Returns**: Array of all garnishments for this employee

#### Sample Response Body:

```javascript
  [
    {
      "id": 1363316536327000
      "version": "63152767c822d6b0385509b973c49dda"
      "employee_id": 8964216891236743
      "active": true
      "amount": "100.00"
      "description": "Child support"
      "court_ordered": true
      "times": null
      "recurring": true
      "annual_maximum": "400.00"
      "pay_period_maximum": null
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

**Endpoint**: `/api/v1/garnishments/:garnishment_id`

**Returns**: Single garnishment representation

#### Sample Response Body:

```javascript
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

**Endpoint**: `/api/v1/employees/:employee_id/garnishments/`

**Returns**: Updated garnishment or errors which prevent update

#### Sample Request Body:

```javascript
  {
    "version": "52b7c567242cb7452e89ba2bc02cb476",
    "active": false
  }
```

## Create a garnishment

**HTTP Method**: `POST`

**Endpoint**: `/api/v1/garnishments/:garnishment_id`

**Returns**: New garnishment or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "employee_id": 8964216891236743
    "amount": "150.00"
    "description": "Back taxes"
    "court_ordered": true
    "recurring": true
    "deduct_as_percentage": false
  }
```
