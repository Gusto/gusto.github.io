---
permalink: v1/contractors
layout: sidebar
title: Contractors
---

# Contractors

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | The unique identifier of this contractor in Gusto.
| `version`                     | String            |     X     |          |         | The version of this object. See <a href="/v1/considerations/versioning">the versioning documentation</a> for a more in depth explanation of versions.
| `company_id`                  | Integer           |     X     |          |         | The ID of the company to which the contractor belongs.
| `type`                        | String            |           |          |         | The contractor type, either an "Individual" or a "Business".
| `start_date`                  | String            |           |          |         | The day when the contractor will start working for the company.
| `is_active`                   | Boolean           |     X     |          |         | The contractor's status with the company. Contractors created through the API will default to active.
| `first_name`                  | String            |           |          |         | The contractor's first name. This attribute is required for "Individual" contractors and will be ignored for "Business" contractors.
| `middle_initial`              | String            |           |    X     | null    | The contractor's middle initial. This attribute is optional for "Individual" contractors and will be ignored for "Business" contractors.
| `last_name`                   | String            |           |          |         | The contractor's last name. This attribute is required for "Individual" contractors and will be ignored for "Business" contractors.
| `email`                       | String            |           |    X     | null    | The contractor's email address. This attribute is optional for "Individual" contractors and will be ignored for "Business" contractors. This attribute should only be included in POST requests. If `email` is included in a PUT request, it will be ignored.
| `self_onboarding`             | Boolean           |           |    X     | false   | Specifies whether the contractor or the administrator will complete onboarding in. Self-onboarding is recommended so that contractors receive Gusto accounts. If `self_onboarding` is true, then `email` is required. This attribute should only be included in POST requests. If `self_onboarding` is included in a PUT request, it will be ignored.
| `business_name`               | String            |           |          |         | The name of the contractor business. This attribute is required for "Business" contractors and will be ignored for "Individual" contractors.
| `ein`                         | String            |           |    X     | null    | The employer identification number of the contractor business. This attribute is optional for "Business" contractors and will be ignored for "Individual" contractors.
| `wage_type`                   | String            |           |          |         | The contractor's wage type, either "Fixed" or "Hourly".
| `hourly_rate`                 | String            |           |    X     |   0.0   | The contractor's hourly rate. This attribute is required if the wage_type is "Hourly".
| `address`                     | Object            |     X     |          |         | The contractor's home address.
| `address:street_1`            | String            |     X     |          |         |
| `address:street_2`            | String            |     X     |          |         |
| `address:city`                | String            |     X     |          |         |
| `address:state`               | String            |     X     |          |         |
| `address:zip`                 | String            |     X     |          |         |

## Get a contractor

**HTTP Method**: `GET`

**Endpoint**: `/v1/contractors/:contractor_id`

**Returns**: The representation of a single contractor.

#### Example Response

```json
{
    "id": 7757515807594512,
    "company_id": 7757616923763477,
    "wage_type": "Fixed",
    "is_active": false,
    "version": "63859768485e218ccf8a449bb60f14ed",
    "type": "Individual",
    "first_name": "Kory",
    "last_name": "Gottlieb",
    "middle_initial": "P",
    "business_name": null,
    "ein": null,
    "email": "keira.west@mckenzie.org",
    "address": {
        "street_1": "621 Jast Row",
        "street_2": "Apt. 281",
        "city": "Coral Springs",
        "state": "FL",
        "zip": "33065",
        "country": "USA"
    },
    "hourly_rate": "0.00"
}
```


## Get contractors for a company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/contractors`

**Returns**: An array of all contractors, active and inactive, for the company.

#### Example Response

```json
[{
    "id": 7757515807594512,
    "company_id": 7757616923763477,
    "wage_type": "Fixed",
    "is_active": false,
    "version": "63859768485e218ccf8a449bb60f14ed",
    "type": "Individual",
    "first_name": "Kory",
    "last_name": "Gottlieb",
    "middle_initial": "P",
    "business_name": null,
    "ein": null,
    "email": "keira.west@mckenzie.org",
    "address": {
        "street_1": "621 Jast Row",
        "street_2": "Apt. 281",
        "city": "Coral Springs",
        "state": "FL",
        "zip": "33065",
        "country": "USA"
    },
    "hourly_rate": "0.00"
},
{
    "id": 7757515807614539,
    "company_id": 7757616923763477,
    "wage_type": "Fixed",
    "is_active": true,
    "version": "8aab307f1e8ed788697f8986346af559",
    "type": "Business",
    "first_name": null,
    "last_name": null,
    "middle_initial": null,
    "business_name": "Labadie-Stroman",
    "ein": "XX-XXX0001",
    "email": "jonatan@kerluke.info",
    "address": {
        "street_1": "1625 Bednar Center",
        "street_2": "Apt. 480",
        "city": "Port Charlotte",
        "state": "FL",
        "zip": "33954",
        "country": "USA"
    },
    "hourly_rate": "0.00"
},
{
    "id": 7757515807623484,
    "company_id": 7757616923763477,
    "wage_type": "Fixed",
    "is_active": true,
    "version": "b48c46abfed1487b873b442334b3c4ff",
    "type": "Individual",
    "first_name": "Chanel",
    "last_name": "Boyle",
    "middle_initial": "X",
    "business_name": null,
    "ein": null,
    "email": "loyal@hettinger.biz",
    "address": {
        "street_1": "35913 Darrick Run",
        "street_2": "Apt. 913",
        "city": "Cypress",
        "state": "TX",
        "zip": "77433",
        "country": "USA"
    },
    "hourly_rate": "0.00"
}]
```

## Create an Individual contractor

**HTTP Method**: `POST`

**Endpoint**: `/v1/companies/:company_id/contractors`

**Returns**: The representation of the created contractor or errors which prevented the creation.

```json
{
    "type": "Individual",
    "wage_type": "Fixed",
    "first_name": "Johnson",
    "last_name": "Johnson",
    "start_date": "2020-04-01",
    "self_onboarding": true,
    "email": "johnson@johnson.com"
}
```

## Create a Business contractor

**HTTP Method**: `POST`

**Endpoint**: `/v1/companies/:company_id/contractors`

**Returns**: The representation of the create contractor or errors which prevented the creation.

```json
{
    "type": "Business",
    "wage_type": "Fixed",
    "business_name": "Johnson-Johnson Contractors",
    "start_date": "2020-04-01"
}
```

## Update a contractor

**HTTP Method**: `PUT`

**Endpoint**: `/v1/contractors/:contractor_id`

**Returns**: The representation of the updated contractor or errors which prevented the update.

```json
{
    "version": "b48c46abfed1487b873b442334b3c4ff",
    "wage_type": "Hourly",
    "hourly_rate": "20.00"
}
```
