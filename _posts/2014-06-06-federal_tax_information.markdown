---
permalink: v1/employee_federal_tax_information
layout: resource
title: Federal Tax Information
---


# Federal Tax Information

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


