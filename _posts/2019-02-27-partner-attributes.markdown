---
permalink: v1/partner_attributes
layout: sidebar
title: Partner Attributes
---

# Partner Attributes

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Description
| :----------                   |:-------------     |:---------:|:--------:|:-------------
| `company_id`                  | String            |     X     |    X     | unique identifier of this company in your system. (Not to be confused with Gusto's company id)
| `user_id`                     | String            |     X     |    X     | unique identifier of the company's primary payroll admin in your system.  
| `grants_rev_share`            | Boolean           |     X     |    X     | 

## Get partner attributes

**HTTP Method**: `GET`

**Endpoint**: `/v1/partner_attributes/:company_id`

**Returns**: Partner-specific information about the company

**Response Codes**:

| Code        | Description
| :---------- |:------------- 
| `200`       | ok
| `404`       | the company was not found or company had no partner details        

#### Sample Response Body:

```json
{
  "company_id": "food-truck-88913",
  "user_id": "person-815932",
  "accounting_firm_id": "firm-3193",
  "grants_rev_share": false
}
```
