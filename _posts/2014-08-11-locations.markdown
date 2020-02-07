---
permalink: v1/locations
layout: sidebar
title: Locations
---


# Locations

Locations represent company addresses inside Gusto.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this company location
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning">the versioning documentation</a> for a more in depth explaination of versions
| `company_id`                 | Integer            |     X     |          |         | id for the company to which this location belongs. Only included if address belongs to a company.
| `phone_number`                | String            |           |          |         | phone number for this location. Required for company locations, optional for employee locations
| `street_1`                    | String            |           |          |         | first line of the address
| `street_2`                    | String            |           |    X     | null    | second line of the address
| `city`                        | String            |           |          |         | city of the address
| `state`                       | String            |           |          |         | state of this address
| `zip`                         | String            |           |          |         | zipcode of this address
| `country`                     | String            |           |    X     | "USA"   | country for this address
| `active`                      | Boolean           |     X     |          |         | status of the address, addresses with `active: false` have been deleted, but may still have historical data associated with them

## Get a location by id

**HTTP Method**: `GET`

**Endpoint**: `/v1/locations/:location_id`

**Returns**: A single location representation

**Response Codes**: 200

### Sample Response Body

```json
{
  "id": 1402342024000,
  "version": "fe75bd065ff48b91c35fe8ff842f986c",
  "phone_number": "8009360383",
  "company_id": 1402341716000,
  "street_1": "21 Stillman Street",
  "street_2": "Apartment 6",
  "city": "San Francisco",
  "state": "CA",
  "zip": "94107",
  "country": "USA"
}
```

## Update a a location by id

**HTTP Method**: `PUT`

**Endpoint**: `/v1/locations/:location_id`

**Returns**: Updated location or errors which prevented update

**Response Codes**: 200, 422

### Sample Request Body

```json
{
  "street_1": "425 2nd Street",
  "street_2": "Suite 602"
}
```
