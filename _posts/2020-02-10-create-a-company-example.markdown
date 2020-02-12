---
permalink: /v1/examples/creating-a-company
title: Creating Companies
layout: sidebar
---

# Creating a Company

## Overview

The company provisioning API provides a way to create a Gusto company as part of your integration. When you successfully call the API, the API does the following:

* Creates a new company in Gusto.
* Creates a new user in Gusto.
* Makes the new user the primary payroll administrator of the new company.
* Sends a welcome email to the new user.

In the response, you will receive an account claim URL. Redirect the user to this URL to complete their account setup inside of Gusto.

## Authentication

Due to the nature of this endpoint, Gusto will provide partners with an API token and will permit partners to use API Token Authentication instead of OAuth to provision Gusto accounts. The API token is included in the authorization HTTP header with the Token scheme, e.g.:

```
Content-Type: application/json
Authorization: Token bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71
```

## Request Documentation

| **Attribute**            | **Type**      | **Required** | **Description**
| :----------              |:-------       |:-------      |:-------------
| user                     | Object        | Y            | Information for the primary payroll administrator for the new company.
| user:first_name          | String        | Y            | First name of the primary payroll admin.
| user:last_name           | String        | Y            | Last name of the primary payroll admin.
| user:email               | String        | Y            | Email for the primary payroll admin. This email will also be used for their login.
| user:phone               | String        | N            | Phone number for the primary payroll admin.
| company                  | Object        | Y            | Information for the new company.
| company:name             | String        | Y            | Legal name of the company.
| company:trade_name       | String        | N            | Name of the company.
| company:ein              | String        | N            | The employer identification number (EIN) of the company.
| company:number_employees | Integer       | N            | The number of employees in the company.
| company:states           | Array[String] | N            | The states in which the company operates.
| company:addresses        | Array[Object] | N            | The locations for the company. This includes mailing, work, and filing addresses.
| address:street_1         | String        | Y            |
| address:street_2         | String        | N            |
| address:city             | String        | Y            |
| address:state            | String        | Y            |
| address:zip              | String        | Y            |
| address:phone            | String        | Y            |
| address:is_primary       | Boolean       | N            | Whether or not this is a primary address for the company. If set to true, the address will be used as the mailing and filing address for the company and will be added as a work location. If set to false or not included, the address will only be added as a work location for the company. If multiple addresses are included, only one should be marked as primary.


## Example Requests

### Minimum Request Payload
```json
{
  "user": {
    "first_name": "Frank",
    "last_name": "Ocean",
    "email": "frank@example.com"
  },
  "company": {
    "name": "Frank's Ocean, LLC"
  }
}
```

### Maximum Request Payload
```json
{
  "user": {
    "first_name": "Frank",
    "last_name": "Ocean",
    "email": "frank@example.com",
    "phone": "2345558899"
  },
  "company": {
    "name": "Frank's Ocean, LLC",
    "trade_name": "Frank’s Ocean",
    "ein": "123456789",
    "states": ["CO", "CA"],
    "number_employees": 8,
    "addresses": [{
      "street_1": "1201 16th Street Mall",
      "street_2": "Suite 350",
      "city": "Denver",
      "zip": "80202",
      "state": "CO",
      "phone": "2345678900",
      "is_primary": "true"
    },{
      "street_1": "525 20th Street",
      "city": "San Francisco",
      "zip": "94107",
      "state": "CA",
      "phone": "2345678901"
    }]
  }
}
```

## Example Response
```json
{
  "account_claim_url": "https://app.gusto.com/claim_account/3456789"
}
```

## Errors

| **Status Code**               | **Description**
| :----------                   |:-------------
| **401 Unauthorized**          | An API token has not been included in the request for authentication.
| **422 Unprocessable Entity**  | We were unable to process the request. Either a required attribute was missing or the user email included in the request payload already exists in Gusto.
| **500 Internal Server Error** | Something went wrong on our end. Please let us know if this happens and forward the request payload that was sent.
