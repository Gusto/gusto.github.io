---
permalink: v1/employees
layout: resource
title: Employees
---

# Employees

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this employee in the ZenPayroll system.
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions.
| `first_name`                  | String            |           |          |         | employee's first name.
| `middle_initial`              | String            |           |    X     | null    | employee's middle initial. Not guaranteed to exist.
| `last_name`                   | String            |           |          |         | employee's last name.
| `email`                       | String            |           |    X     | null    | employee's email address. This is provided specifically to sync users between our system and yours. You may not use this address for any other purpose (e.g. marketing.) Not guaranteed to exist.
| `ssn`                         | String            |           |    X     | null    | masked social security number. When updating this attribute, format should be a string of nine numbers (no dashes.)
| `date_of_birth`               | String            |           |    X     | null    | employee's birthday!
| `jobs`                        | Array             |     X     |          |         | array of job information. See <a href="/v1/jobs">jobs documentation</a> for full documentation and endpoints.
| `home_address`                | Object            |     X     |          |         | employee's home address. See <a href="/v1/employee_home_address">employee home address documentation</a> for full documentation and endpoints.
| `federal_tax_information`     | Object            |     X     |          |         | employee's federal tax information. See <a href="/v1/employee_federal_tax_information">employee federal tax information documentation</a> for full documentation and endpoints.
| `garnishments`                | Array             |     X     |          |         | array of garnishments. See <a href="/v1/garnishments">garnishments documentation</a> for full documentation and endpoints.
| `eligible_paid_time_off`      | Array             |     X     |          |         | array of paid time off information. See <a href="/v1/paid_time_off">paid time off documentation</a> for full documentation and endpoints.
| `terminated`                  | Boolean           |     X     |          |         | whether the employee has been terminated from the company.
| `terminations`                | Array             |     X     |          |         | array of terminations for this employee
| `active`                      | Boolean           |     X     |          |         | whether this termination is currently in effect
| `effective_date`              | String            |     X     |          |         | The employee's last day of work at the company
| `run_termination_payroll`     | Boolean           |     X     |          |         | If true, employee will recieve their last, prorated wages via an offcycle payroll. If false, they will recieve their final wages with the rest of the company


## Get an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/companies/:company_id/employees`

**Returns**: Array of all employees currently employeed with this company.

#### Sample Response Body:

```javascript
  {
    "id" : 1123581321345589,
    "version" : "db0edd04aaac4506f7edab03ac855d56",
    "first_name" : "Soren",
    "middle_initial" : "A",
    "last_name" : "Kierkegaard",
    "email" : "knight0faith@initech.biz",
    "ssn" : "XXX-XX-2940",
    "date_of_birth" : "1813-05-05",
    "jobs" : [
      {
        "id" : 1,
        "title" : "Underwater Basket Weaver",
        "rate" : "80000.00",
        "payment_unit" : "Year",
        "location_id" : 3141592653589793
      }
    ],
    "home_address" : {
      "id" : 1402342024000
      "version" : "fe75bd065ff48b91c35fe8ff842f986c",
      "employee_id" : 1123581321345589,
      "street_1": "425 2nd Street",
      "street_2": "Suite 602",
      "city" : "San Francisco",
      "state" : "CA",
      "zip" : "94107",
      "country" : "USA"
    },
    "federal_tax_information" :   {
      "version" : "6e177399876585d0dc493e439c00d18e",
      "employee_id" : 1123581321345589,
      "withholding_allowance" : 2,
      "additional_withholding" : "0.00"
      "filing_status" : "Single",
      "decline_withholding" : false
    },
    "garnishments" : [
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
    "eligible_paid_time_off" : [],
    "terminated" : false,
    "terminations" : []
  }
```


## Get employees for a company

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/companies/:company_id/employees`

**Returns**: Array of all employees currently employeed with this company.

#### Sample Response Body:

```javascript
  [
    {
      "id" : 1123581321345589,
      "version" : "db0edd04aaac4506f7edab03ac855d56",
      "first_name" : "Soren",
      "middle_initial" : "A",
      "last_name" : "Kierkegaard",
      "email" : "knight0faith@initech.biz",
      "ssn" : "XXX-XX-2940",
      "date_of_birth" : "1813-05-05",
      "jobs" : [
        {
          "id" : 1,
          "title" : "Underwater Basket Weaver",
          "rate" : "80000.00",
          "payment_unit" : "Year",
          "location_id" : 3141592653589793
        }
      ],
      "home_address" : {
        "id" : 1402342024000
        "version" : "fe75bd065ff48b91c35fe8ff842f986c",
        "employee_id" : 1123581321345589,
        "street_1": "425 2nd Street",
        "street_2": "Suite 602",
        "city" : "San Francisco",
        "state" : "CA",
        "zip" : "94107",
        "country" : "USA"
      },
      "federal_tax_information" :   {
        "version" : "6e177399876585d0dc493e439c00d18e",
        "employee_id" : 1123581321345589,
        "withholding_allowance" : 2,
        "additional_withholding" : "0.00"
        "filing_status" : "Single",
        "decline_withholding" : false
      },
      "garnishments" : [
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
      "eligible_paid_time_off" : [],
      "terminated" : false,
      "terminations" : []
    }
  ]
```

### Optional Parameters

You can pare down the results by passing in additional parameters:

  Available options: terminated

    GET /api/v1/companies/3337/employees?terminated=false
      => returns all employees that have not been terminated

## Update an employee

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/employees/:employee_id`

**Returns**: Updated employee or errors which prevented update

#### Sample Request Body:

```javascript
  {
    "version" : "db0edd04aaac4506f7edab03ac855d56",
    "middle_initial" : "Q",
    "email" : "knight0faith@initech.biz",
    "ssn" : "1234562940"
  }
```

## Create an employee

**HTTP Method**: `POST`

**Endpoint**: `/api/v1/companies/:company_id/employees`

**Returns**: Created employee or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "first_name" : "Isaiah",
    "last_name"  : "Berlin",
    "email" : "crooked-timber@initech.biz"
  }
```
