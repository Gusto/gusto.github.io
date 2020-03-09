---
permalink: v1/companies
title: Companies
layout: sidebar
---

# Companies

## Get Company Information

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id`

**Returns**: Get information about a particular company

```json
{
  "id": 2357111317192329,
  "name": "Ye Olde Wig Shoppe",
  "trade_name": "Fezziwig's",
  "ein": "12-3456789",
  "entity_type": "LLC",
  "company_status": "Approved",
  "locations": [
    {
      "id": 3141592653589793,
      "street_1": "450 Serra Mall",
      "street_2": "Department of Philosophy",
      "city": "Stanford",
      "state": "CA",
      "zip": "94305"
    },
    {
      "id": 2718281828459045,
      "street_1": "314 Moses Hall #2390",
      "street_2": "University of California",
      "city": "Berkeley",
      "state": "CA",
      "zip": "94720"
    }
  ],
  "compensations": {
    "hourly": [
      {
        "name": "Regular Hours",
        "multiple": 1
      },
      {
        "name": "Overtime",
        "multiple": 1.5
      },
      {
        "name": "Double Overtime",
        "multiple": 2
      }
    ],
    "fixed": [
      {
        "name": "Bonus"
      },
      {
        "name": "Commission"
      }
    ],
    "paid_time_off": [
      {
        "name": "Vacation Hours"
      },
      {
        "name": "Sick Hours"
      }
    ]
  },
  "primary_signatory": {
    "first_name": "Isaiah",
    "middle_initial": "H",
    "last_name"  : "Berlin",
    "phone": "8001234567",
    "email": "crooked-timber@initech.biz",
    "home_address": {
      "street_1": "314 Moses Hall #2390",
      "street_2": "University of California",
      "city": "Berkeley",
      "state": "CA",
      "zip": "94720",
      "country": "USA"
    }
  },
  "primary_payroll_admin": {
    "first_name": "Isaiah",
    "last_name"  : "Berlin",
    "phone": "8001234567",
    "email": "crooked-timber@initech.biz"
  }
}
```

| Attribute                          | Type                           | Description
| :----------                        |:-------------                  |:-------------
| `id`                               | Integer                        | The unique identifier of this company in the Gusto system.
| `name`                             | String                         | The name of this company.
| `trade_name`                       | String                         | The trade name of this company. This is an optional field.
| `ein`                              | String                         | The employer identification number for this company.
| `entity_type`                      | String                         | The type of the company (e.g. "LLC").
| `company_status`                   | String                         | The status of the company, one of: "Approved", "Not Approved", "Suspended".<br/><br/>"Approved": The company is approved to run payroll with Gusto.<br/><br/>"Not Approved": The company is not approved to run payroll with Gusto. In order to run payroll, the company needs to either complete onboarding or contact Gusto support.<br/><br/>"Suspended": The company's Gusto account is suspended and they cannot currently run payroll. In order to unsuspend their account, the company must contact Gusto support.
| `locations`                        | Array[Address]                 | The locations for the company.
| `address:id`                       | String                         | The identifier of this location in the Gusto system.
| `address:street_1`                 | String                         | The first street of the address.
| `address:street_2`                 | String                         | The second street of the address.
| `address:city`                     | String                         | The city of the address.
| `address:state`                    | String                         | The two letter state abbreviation of the address.
| `address:zip`                      | String                         | The five digit zipcode of the address.
| `compensations`                    | Object                         | An object containing all available company-wide compensations. The above compensations are the default, built-in compensations.
| `compensations:hourly`             | Array[HourlyCompensation]      | An array of available hourly compensations.
| `compensations:hourly:name`        | String                         | The name of the hourly compensation.
| `compensations:hourly:multiple`    | Integer                        | The amount multiplied by the base rate of a given job to calculate total compensation per hour worked. For example, if an employee at this company makes $17.00/hour and works 10 hours of Overtime (which has a multiple of 1.5), they would expect to receive $150.
| `compensations:fixed`              | Array[FixedCompensation]       | An array of available fixed compensations.
| `compensations:fixed:name`         | String                         | The name of the fixed compensation.  
| `compensations:paid_time_off`      | Array[PaidTimeOffCompensation] | An array of available types of paid time off.
| `compensations:paid_time_off:name` | String                         | The name of the time off.
| `primary_signatory`                | Object                         | An object representing the primary signatory of the company.  
| `primary_signatory:first_name`     | String                         | The primary signatory's first name.
| `primary_signatory:middle_initial` | String                         | The primary signatory's middle initial.
| `primary_signatory:last_name`      | String                         | The primary signatory's last name.
| `primary_signatory:phone`          | String                         | The primary signatory's phone number.
| `primary_signatory:email`          | String                         | The primary signatory's email.
| `primary_signatory:home_address`   | String                         | The primary signatory's home address.
| `primary_payroll_admin`            | Object                         | An object representing the primary payroll administrator of the company.
| `primary_payroll_admin:first_name` | String                         | The primary payroll admin's first name.
| `primary_payroll_admin:last_name`  | String                         | The primary payroll admin's last name.
| `primary_payroll_admin:phone`      | String                         | The primary payroll admin's phone number.
| `primary_payroll_admin:email`      | String                         | The primary payroll admin's email.
