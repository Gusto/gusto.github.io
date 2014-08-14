---
permalink: v1/company_locations
layout: resource
title: Company Locations
---


# Company Locations

Company locations represent all addresses associated with a company. These can
be filing addesses, mailing addresses, and/or work locations; one address may
serve multiple, or all, purposes.

Since all company locations are subsets of <a href="/v1/locations">locations</a>,
retrieving or updating an individual record should be done via the <a href="/v1/locations">locations</a> endpoints.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this company location
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `company_id`                  | Integer            |     X     |          |         | id for the company to which this location belongs
| `phone_number`                | String             |           |          |         | Phone number for this company location. Formatted as ten digits
| `street_1`                    | String            |           |          |         | first line of the address
| `street_2`                    | String            |           |    X     | null    | second line of the address
| `city`                        | String            |           |          |         | city of the address
| `state`                       | String            |           |          |         | state of this address
| `zip`                         | String            |           |          |         | zipcode of this address
| `country`                     | String            |           |    X     | "USA"   | country for this address

## Get company locations for a company

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/companies/:company_id/locations`

**Returns**: Array of all locations for this company

**Response Codes**: 200

### Sample Response Body

```javascript
[
  {
    "id" : 1402342024000
    "version" : "fe75bd065ff48b91c35fe8ff842f986c",
    "company_id" : 1402341716000,
    "phone_number" : "8009360383",
    "street_1": "425 2nd Street",
    "street_2": "Suite 602",
    "city" : "San Francisco",
    "state" : "CA",
    "zip" : "94107",
    "country" : "USA"
  }
]
```

## Create a company location for a given company

**HTTP Method**: `POST`

**Endpoint**: `/api/v1/companies/:company_id/locations`

**Returns**: Newly created company location or errors which prevented creation

**Response Codes**: 200, 422

### Sample Request Body

```javascript
[
  {
    "phone_number" : "8009360383",
    "street_1": "425 2nd Street",
    "street_2": "Suite 602",
    "city" : "San Francisco",
    "state" : "CA",
    "zip" : "94107",
    "country" : "USA"
  }
]
```
