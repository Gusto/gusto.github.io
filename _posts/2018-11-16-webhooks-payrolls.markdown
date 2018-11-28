---
permalink: v1/webhooks/payrolls
title: Payrolls Webhooks
layout: sidebar
---

# Payrolls Webhooks

## Get Payroll Webhook Notifications
[Webhooks Overview](/v1/webhooks/about)

**Resource**: `Company`

**Entity**: `Payroll` ([API Reference](/v1/payrolls))


**Event Types**:

- `payroll.created`

- `payroll.updated`

**Note** We do not currently have an endpoint for fetching a singular payroll. Until this gets developed, fetching the equivalent data from the public API will require fetching from the index endpoint. You can read more about scoping the request down to reduce the amount of noise [here](http://docs.gusto.com/v1/payrolls). Specifically, you may find the optional `start_date` and `end_date` useful for retrieving a specific payroll from this webhook event.

**Returns**: Get information about a particular payroll that was created or updated

```json
{
  "event_type": "payroll.created",
  "resource_type": "Company",
  "resource_id": 7757616923531095,
  "entity_type": "Payroll",
  "entity_id": 1,
  "timestamp": 1533606328,
  "entity_attributes": {
    "version": "19289df18e6e20f797de4a585ea5a91535c7ddf7",
    "payroll_deadline": "2018-02-18",
    "processed": true,
    "pay_period": {
      "start_date": "2018-02-01",
      "end_date": "2018-02-15",
      "pay_schedule_id": 7757500908984137
    },
    "totals": {
      "company_debit": "2791.25",
      "reimbursements": "0.00",
      "net_pay": "1953.31",
      "correction": "0.00",
      "employer_taxes": "191.25",
      "employee_taxes": "646.69",
      "benefits": "0.0"
    },
    "employee_compensations": [
      {
        "employee_id": 1123581321345589,
        "gross_pay": "2791.25",
        "net_pay": "1953.31",
        "payment_method": "Direct Deposit",
        "fixed_compensations": [
          {
            "name": "Bonus",
            "amount": "100.00",
            "job_id": 1
          },
          {
            "name": "Reimbursement",
            "amount": "100.00",
            "job_id": 1
          }
        ],
        "hourly_compensations": [
          {
            "name": "Regular Hours",
            "hours": "40.000",
            "job_id": 1,
            "compensation_multiplier": 1
          },
          {
            "name": "Overtime",
            "hours": "15.000",
            "job_id": 1,
            "compensation_multiplier": 1.5
          },
          {
            "name": "Double Overtime",
            "hours": "0.000",
            "job_id": 1,
            "compensation_multiplier": 2
          },
          {
            "name": "Regular Hours",
            "hours": "40.000",
            "job_id": 2,
            "compensation_multiplier": 1
          },
          {
            "name": "Overtime",
            "hours": "5.000",
            "job_id": 2,
            "compensation_multiplier": 1.5
          },
          {
            "name": "Double Overtime",
            "hours": "0.000",
            "job_id": 2,
            "compensation_multiplier": 2
          }
        ],
        "paid_time_off": [
          {
            "name": "Vacation Hours",
            "hours": "20.000"
          },
          {
            "name": "Sick Hours",
            "hours": "0.000"
          },
          {
            "name": "Holiday Hours",
            "hours": "0.000"
          }
        ],
        "benefits": [],
        "taxes": [
          {
            "name": "Federal Income Tax",
            "employer": false,
            "amount": "646.69"
          },
          {
            "name": "Social Security",
            "employer": true,
            "amount": "191.25"
          }
        ]
      }
    ]
  }
}
```
