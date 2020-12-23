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
| `contractor_payments:payments:payment_method` | String            |     X     |          |         | The payment method.
| `contractor_payments:payments:reimbursement`  | String            |     X     |          |         | The payment reimbursement.
| `contractor_payments:payments:wage`           | String            |     X     |          |         | The payment wage.
| `contractor_payments:payments:wage_type`      | String            |     X     |          |         | The wage type.


## Get contractor payments for a given company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/contractor_payments?start_date=2020-01-01&end_date=2020-12-31`

**Returns**: An object containing individual contractor payments, within a given time period, including totals.

#### Example Response

```json
{
  "total": {
    "reimbursements": "100.0",
    "wages": "740.0"
  },
  "contractor_payments": [
    {
      "contractor_id": 1234,
      "reimbursement_total": "100.0",
      "wage_total": "740.0",
      "payments": [
        {
          "bonus": "20.0",
          "date": "2020-10-19",
          "hours": "40.0",
          "payment_method": "Historical Payment",
          "reimbursement": "100.0",
          "wage": "0.0",
          "wage_type": "Hourly"
        }
      ]
    }
  ]
}
```
