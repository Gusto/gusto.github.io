---
permalink: v1/employee_federal_tax_information
layout: resource
title: Federal Tax Information
---

# Federal Tax Information

Federal tax information for an employee. Most information will be provided by employees during their onboarding process

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `employee_id`                 | Integer           |     X     |          |         | id of the employee to which this tax information belongs
| `withholding_allowance`       | Integer           |           |          |         | Allowance used to calculate federal tax withholdings if `filing_status` is not 'Exempt' and `decline_withholdings` is not true. Should be from 1-99. Employees should use the <a href="http://www.irs.gov/pub/irs-pdf/fw4.pdf" target="_blank">W-4 worksheet</a> to calculate this number, or use the online <a href="http://apps.irs.gov/app/withholdingcalculator/">IRS calculator</a>. Generally, the higher the federal withholding allowance, the less tax is withheld with each paycheck
| `additional_withholding`      | String            |           |    X     | "0.00"  | An additional fixed amount that should be withheld for Federal taxes each pay period
| `filing_status`               | String            |           |          |         | Employees that elect 'Exempt' will not withhold federal income tax, but wages will still be reported on the W-2. One of 'Single', 'Married', 'Married, but withhold as Single', or 'Exempt'
| `decline_withholding`         | Boolean           |           |    X     | false   | If the employee has asked that no withholdings be taken out. This is not the same as Filing Status being 'Exempt'. In this case, the employee owes federal taxes but is electing not to have any taxes withheld from their paycheck

## Get federal tax information for an employee

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/employees/:employee_id/federal_tax_information`

**Returns**: Federal tax information for a particular employee

#### Sample Response Body:

```javascript
  {
    "version" : "6e177399876585d0dc493e439c00d18e",
    "employee_id" : 1402341716000,
    "withholding_allowance" : 2,
    "additional_withholding" : "0.00"
    "filing_status" : "Single",
    "decline_withholding" : false
  }
```

## Update federal tax information for an employee

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/employees/:employee_id/federal_tax_information`

**Returns**: Updated federal tax information or errors which prevented update

#### Sample Response Body:

```javascript
  {
    "version" : "6e177399876585d0dc493e439c00d18e",
    "filing_status" : "Married",
    "decline_withholding" : true
  }
```


