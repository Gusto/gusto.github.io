---
permalink: v1/ytd_benefit_amounts_from_different_company
layout: sidebar
title: Year-to-date Benefit Amounts from Different Company
---

# Year-to-date Benefit Amounts from Different Company
### This endpoint is under development and does not yet exist



Year-to-date benefit amounts from a different company represents the amount of money added to an employees plan during a current year, made outside of the current contribution when they were employed at a different company.

## Attributes

| Attribute                         | Type          | Read-Only | Optional | Default | Description
| :----------                       |:------------- |:---------:|:--------:|:--------|:-------------
| `benefit_id`                      | Integer       |           |          |         | The id for the benefit got from the <a href="/v1/benefits">benefits api.
| `tax_year`                        | Integer       |           |          |         | The tax year for which this amount applies.
| `ytd_employee_deduction_amount`   | Float         |           |          |         | The year-to-date employee deduction made outside the current company.
| `ytd_company_contribution_amount` | Float         |           |          |         | The year-to-date company contribution made outside the current company.

## Set the contribution and deduction amounts for an employee benefits made at a different company

**HTTP Method**: `POST`

**Endpoint**: `/v1/employees/:employee_id/ytd_benefit_amounts_from_different_company`

**Returns**: HTTP Status Code 204 (No Content) or errors which prevented creation
