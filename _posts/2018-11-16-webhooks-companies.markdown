---
permalink: v1/webhooks/companies
title: Companies Webhooks
layout: sidebar
---

# Companies Webhooks

## Get Company Webhook Notifications

[Webhooks Overview](/v1/webhooks/about)

**Endpoint**: `GET /v1/companies/:company_id`

Use this endpoint to retrieve the information given in these webhook events using our public API. For more information about the endpoint, please refer to the endpoint's [documentation](/v1/companies).


**Resource**: `Company`

**Entity**: `Company`


**Event Types**:

- `company.provisioned`

- `company.updated`

- `company.deprovisioned`

**Returns**: Get information about a particular company that was created or updated

```json
{
  "event_type": "company.provisioned",
  "resource_type": "Company",
  "resource_id": 7757500908984137,
  "entity_type": "Company",
  "entity_id": 7757500908984137,
  "timestamp": 1533606328,
  "entity_attributes": {
    "id": 7757500908984137,
    "name": "Ye Olde Wig Shoppe",
    "trade_name": "Fezziwig's",
    "ein": "12-3456789",
    "entity_type": "LLC",
    "industry_code": "0001",
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
}
```

```json
{
  "event_type": "company.deprovisioned",
  "resource_type": "Company",
  "resource_id": 7757500908984137,
  "entity_type": "Company",
  "entity_id": 7757500908984137,
  "timestamp": 1533606328,
  "entity_attributes": {
    "company_id": 7757500908984137
  }
}
```
