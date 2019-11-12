---
permalink: v1/employees
layout: sidebar
title: Employees
---

# Employees

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this employee in the Gusto system.
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning">the versioning documentation</a> for a more in depth explaination of versions.
| `first_name`                  | String            |           |          |         | employee's first name.
| `middle_initial`              | String            |           |    X     | null    | employee's middle initial. Not guaranteed to exist.
| `last_name`                   | String            |           |          |         | employee's last name.
| `email`                       | String            |           |    X     | null    | employee's email address. This is provided specifically to sync users between our system and yours. You may not use this address for any other purpose (e.g. marketing.) Not guaranteed to exist.
| `company_id`                  | Integer           |     X     |          |         | employee's company ID
| `manager_id`                  | Integer           |     X     |          | null    | employee's manager ID
| `department`                  | String            |     X     |          | null    | employee's department.
| `ssn`                         | String            |           |    X     | null    | masked social security number. When updating this attribute, format should be a string of nine numbers (no dashes.)
| `date_of_birth`               | String            |           |    X     | null    | employee's birthday!
| `jobs`                        | Array             |     X     |          |         | array of job information. See <a href="/v1/jobs">jobs documentation</a> for full documentation and endpoints.
| `home_address`                | Object            |     X     |          |         | employee's home address. See <a href="/v1/employee_home_address">employee home address documentation</a> for full documentation and endpoints.
| `garnishments`                | Array             |     X     |          |         | array of garnishments. See <a href="/v1/garnishments">garnishments documentation</a> for full documentation and endpoints.
| `eligible_paid_time_off`      | Array             |     X     |          |         | array of paid time off information. See <a href="/v1/paid_time_off">paid time off documentation</a> for full documentation and endpoints.
| `onboarded`                   | Boolean           |     X     |          |         | whether the employee is fully onboarded.
| `terminated`                  | Boolean           |     X     |          |         | whether the employee has been terminated from the company.
| `terminations`                | Array             |     X     |          |         | array of terminations for this employee. See <a href="/v1/terminations">terminations documentation</a> for full documentation and endpoints.
| `two_percent_shareholder`     | Boolean           |           |    X     |  false  | Whether the employee is a two percent shareholder of an S-Corp for tax purposes. For `POST` requests, the API returns a 422 error if this attribute is in the request body. For `PUT` requests, the API returns a 422 error if the employee's company is not an S-Corp.

## Get an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/employees/:employee_id`

**Returns**: Receive a single employee representation

#### Sample Response Body:

```json
{
  "id": 1123581321345589,
  "version": "db0edd04aaac4506f7edab03ac855d56",
  "first_name": "Soren",
  "middle_initial": "A",
  "last_name": "Kierkegaard",
  "company_id": 7757616923531095,
  "manager_id": 7757869431804236,
  "department": "Marketing",
  "email": "knight0faith@initech.biz",
  "ssn": "XXX-XX-2940",
  "date_of_birth": "1990-05-05",
  "jobs": [
    {
      "id": 1,
      "title": "Underwater Basket Weaver",
      "rate": "80000.00",
      "payment_unit": "Year",
      "location_id": 3141592653589793
    }
  ],
  "home_address": {
    "id": 1402342024000,
    "version": "fe75bd065ff48b91c35fe8ff842f986c",
    "employee_id": 1123581321345589,
    "street_1": "425 2nd Street",
    "street_2": "Suite 602",
    "city": "San Francisco",
    "state": "CA",
    "zip": "94107",
    "country": "USA"
  },
  "garnishments": [
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
  ],
  "eligible_paid_time_off": [],
  "onboarded": true,
  "terminated": false,
  "terminations": []
}
```


## Get employees for a company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/employees`

**Returns**: Array of all employees currently employeed with this company.

#### Sample Response Body:

```json
[
  {
    "id": 1123581321345589,
    "version": "db0edd04aaac4506f7edab03ac855d56",
    "first_name": "Soren",
    "middle_initial": "A",
    "last_name": "Kierkegaard",
    "company_id": 7757616923531095,
    "manager_id": 7757869431804236,
    "department": "Marketing",
    "email": "knight0faith@initech.biz",
    "ssn": "XXX-XX-2940",
    "date_of_birth": "1990-05-05",
    "jobs": [
      {
        "id": 1,
        "title": "Underwater Basket Weaver",
        "rate": "80000.00",
        "payment_unit": "Year",
        "location_id": 3141592653589793
      }
    ],
    "home_address": {
      "id": 1402342024000,
      "version": "fe75bd065ff48b91c35fe8ff842f986c",
      "employee_id": 1123581321345589,
      "street_1": "425 2nd Street",
      "street_2": "Suite 602",
      "city": "San Francisco",
      "state": "CA",
      "zip": "94107",
      "country": "USA"
    },
    "garnishments": [
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
    ],
    "eligible_paid_time_off": [],
    "onboarded": true,
    "terminated": false,
    "terminations": []
  }
]
```

### Optional Parameters

You can pare down the results by passing in additional parameters:

  Available options: terminated

    GET /v1/companies/3337/employees?terminated=false
      => returns all employees that have not been terminated

## Update an employee

**HTTP Method**: `PUT`

**Endpoint**: `/v1/employees/:employee_id`

**Returns**: Updated employee or errors which prevented update.

**Note**: The `two_percent_shareholder` attribute is only used for employees of S-Corp companies. If the employee's company is not an S-Corp, the API returns a 422 error.

#### Sample Request Body:

```json
{
  "version": "db0edd04aaac4506f7edab03ac855d56",
  "middle_initial": "Q",
  "email": "knight0faith@initech.biz",
  "ssn": "1234562940"
}
```

## Create an employee

**HTTP Method**: `POST`

**Endpoint**: `/v1/companies/:company_id/employees`

**Returns**: Created employee or errors which prevented creation.

**Note**: The `two_percent_shareholder` attribute is not allowed in POST requests. If included, the API returns a 422 error.

#### Sample Request Body:

```json
{
  "first_name": "Isaiah",
  "last_name"  : "Berlin",
  "email": "crooked-timber@initech.biz"
}
```
