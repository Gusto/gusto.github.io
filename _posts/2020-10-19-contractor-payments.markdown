---
permalink: v1/companies/contractor_payments
layout: sidebar
title: Contractor Payments
---

# Contractor Payments

## Attributes

| Attribute                                     | Type              | Read-Only | Optional | Default | Description
| :----------                                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `totals`                                      | Object            |     X     |          |         | The wage and reimbursement totals for all contractor payments within the time period.
| `totals:wages`                                | String            |     X     |          |         | The total wages for contractor payments within the time period.
| `totals:reimbursements`                       | String            |     X     |          |         | The total reimbursements for contractor payments within the time period.
| `contractor_payments`                         | Array             |     X     |          |         | The individual contractor payments, within the time period, grouped by contractor.
| `contractor_payments:contractor_id`           | Integer           |     X     |          |         | The contractor's id
| `contractor_payments:wage_total`              | String            |     X     |          |         | The total wages for a contractor within the given time period.
| `contractor_payments:reimbursement_total`     | String            |     X     |          |         | The total reimbursements for a contractor within the given time period.
| `contractor_payments:payments`                | Array             |     X     |          |         | The contractor's payments within the given time period.
| `contractor_payments:payments:bonus`          | String            |     X     |          |         | The payment bonus.
| `contractor_payments:payments:date`           | String            |     X     |          |         | The payment date.
| `contractor_payments:payments:hours`          | String            |     X     |          |         | The number of hours worked.
| `contractor_payments:payments:payment_method` | String            |     X     |          |         | The payment method ("Direct Deposit", "Check", "Historical Payment", "Correction Payment")
| `contractor_payments:payments:reimbursement`  | String            |     X     |          |         | The payment reimbursement.
| `contractor_payments:payments:hourly_rate`    | String            |     X     |          |         | The rate per hour worked.
| `contractor_payments:payments:wage`           | String            |     X     |          |         | The payment fixed wage, regardles of hours worked.
| `contractor_payments:payments:wage_type`      | String            |     X     |          |         | The wage type ("Hourly", "Fixed")
| `contractor_payments:payments:wage_total`     | String            |     X     |          |         | The sum of the hours worked × hourly rate, wage and bonus


## Get contractor payments for a given company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/contractor_payments?start_date=2020-01-01&end_date=2020-12-31`

**Returns**: An object containing individual contractor payments, within a given time period, including totals.

#### Example Response

```json
{
  "total": {
    "reimbursements": "110.0",
    "wages": "1840.0"
  },
  "contractor_payments": [
    {
      "contractor_id": 1234,
      "reimbursement_total": "110.0",
      "wage_total": "1840.0",
      "payments": [
        {
          "bonus": "20.0",
          "date": "2020-10-19",
          "hours": "40.0",
          "payment_method": "Historical Payment",
          "reimbursement": "100.0",
          "hourly_rate": "18.0",
          "wage": "0.0",
          "wage_type": "Hourly",
          "wage_total": "740.00"
        },
        {
          "bonus": "100.0",
          "date": "2020-10-19",
          "hours": "0.00",
          "payment_method": "Historical Payment",
          "reimbursement": "10.0",
          "hourly_rate": "0.0",
          "wage": "1000.0",
          "wage_type": "Fixed",
          "wage_total": "1100.0"
        }
      ]
    }
  ]
}
```
