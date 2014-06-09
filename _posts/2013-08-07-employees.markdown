---
permalink: v1/employees
layout: resource
title: Employees
---

# Employees

## Get employees for a company

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/companies/:company_id/employees`

**Returns**: Array of all employees currently employeed with this company.

#### Sample Response Body:

```javascript
    [
      {
        "id" : 1123581321345589,
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

| Field                     | Description
| :----------               |:-------------
| `id`                      | the unique identifier of this employee in the ZenPayroll system.
| `first_name`              | employee's first name.
| `middle_initial`          | employee's middle initial. Not guaranteed to exist.
| `last_name`               | employee's last name.
| `email`                   | employee's email address. This is provided specifically to sync users between our system and yours. You may not use this address for any other purpose (e.g. marketing.) Not guaranteed to exist.
| `ssn`                     | masked social security number
| `date_of_birth`           | employee's birthday!
| `jobs`                    | array of job information. See <a href="/v1/jobs">jobs documentation</a> for full documentation and endpoints.
| `home_address`            | employee's home address. See <a href="/v1/employee_home_address
">employee home address documentation</a> for full documentation and endpoints.
| `federal_tax_information`            | employee's federal tax information. See <a href="/v1/employee_federal_tax_information">employee federal tax information documentation</a> for full documentation and endpoints.
| `garnishments`            | array of garnishments. See <a href="/v1/garnishments">garnishments documentation</a> for full documentation and endpoints.
| `terminated`              | whether the employee has been terminated from the company.
| `terminations`            | array of terminations for this employee
| `active`                  | Whether this termination is currently in effect
| `effective_date`          | The employee's last day of work at the company
| `run_termination_payroll` | If true, employee will recieve their last, prorated wages via an offcycle payroll. If false, they will recieve their final wages with the rest of the company
| `eligible_paid_time_off`  | array of paid time off information. See <a href="/v1/paid_time_off">paid time off documentation</a> for full documentation and endpoints.

### Optional Parameters

You can pare down the results by passing in additional parameters:

  Available options: terminated

    GET /api/v1/companies/3337/employees?terminated=false
      => returns all employees that have not been terminated
