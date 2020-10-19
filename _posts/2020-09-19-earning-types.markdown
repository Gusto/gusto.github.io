---
permalink: /v1/earning-types
title: Earning types
layout: sidebar
---

# Earning types

A payroll item in Gusto is associated to an earning type to name the type of earning described by the payroll item.

## Default vs Custom earning types

### Default earning types
Certain earning types are special because they have tax considerations. Those earning types are mostly the same for every company depending on its legal structure (LLC, Corporation, etc.)

### Custom earning types
Custom earning types are all the other earning types added specifically for a company. They are all treated as bonuses for tax purposes.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `uuid`                        | String            |     X     |          |         | the unique identifier of this earning type
| `name`                        | String            |           |          |         | name of this earning type

## Get earning types for a company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/earning_types`

**Returns**: Two array containing the default and custom earning types.

#### Sample Response Body:

```json
{
  "default": [
    {
      "name": "Cash Tips",
      "uuid": "f5618c94-ed7d-4366-b2c4-ff05e430064f"
    }
  ],
  "custom": [
    {
      "name": "Custom earning type",
      "uuid": "6b4a8efb-db90-4c13-a75f-aae11b3f4ff9"
    }
  ]
}
```


## Create earning types for a company

**HTTP Method**: `POST`

**Endpoint**: `/v1/companies/:company_id/earning_types`

**Returns**: The new earning type or errors which prevented creation

If an inactive earning type exists with the same name, it will reactivate it instead of creating a new one.

#### Sample Request Body:

```json
{
  "name": "Custom earning type",
  "uuid": "f4dc8972-8830-4c07-b623-349a04b040d7"
}
```


## Update earning types for a company

**HTTP Method**: `PUT`

**Endpoint**: `/v1/companies/:company_id/earning_types/:earning_type_uuid`

**Returns**: The updated earning type or errors which prevented creation

#### Sample Request Body:

```json
{
  "name": "Custom earning type",
  "uuid": "f4dc8972-8830-4c07-b623-349a04b040d7"
}
```

## Deactivate earning types for a company

**HTTP Method**: `DELETE`

**Endpoint**: `/v1/companies/:company_id/earning_types/:earning_type_uuid`

**Returns**: 204 No content status

It only deactivates the earning type, not a full deletion. Creating an earning type with the same name reactivate it.
