---
permalink: v1/webhooks/employees
title: Employees Webhooks
layout: sidebar
---

# Employees Webhooks

## Get Employee Webhook Notifications
[Webhooks Overview](/v1/webhooks/about)

**Endpoint**: `GET /v1/employees/:employee_id`

Use this endpoint to retrieve the information given in these webhook events using our public API. For more information about the endpoint, please refer to the endpoint's [documentation](/v1/employees).


**Resource**: `Company`

**Entity**: `Employee`


**Event Types**:

- `employee.created`

- `employee.updated`

**Returns**: Get information about a particular employee that was created or updated

```json
{
  "event_type": "employee.created",
  "resource_type": "Company",
  "resource_id": 7757616923531095,
  "entity_type": "Employee",
  "entity_id": 1123581321345589,
  "timestamp": 1533606328,
  "entity_attributes": {
    "id": 1123581321345589,
    "version": "db0edd04aaac4506f7edab03ac855d56",
    "first_name": "Soren",
    "middle_initial": "A",
    "last_name": "Kierkegaard",
    "company_id": 7757616923531095,
    "manager_id": 7757869431804236,
    "department": "Marketing",
    "email": "knight0faith@initech.biz",
    "ssn": "XXX-XX-2940",
    "date_of_birth": "1990-05-05",
    "jobs": [
      {
        "id": 1,
        "title": "Underwater Basket Weaver",
        "rate": "80000.00",
        "payment_unit": "Year",
        "location_id": 3141592653589793
      }
    ],
    "home_address": {
      "id": 1402342024000,
      "version": "fe75bd065ff48b91c35fe8ff842f986c",
      "employee_id": 1123581321345589,
      "street_1": "425 2nd Street",
      "street_2": "Suite 602",
      "city": "San Francisco",
      "state": "CA",
      "zip": "94107",
      "country": "USA"
    },
    "garnishments": [
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
    "eligible_paid_time_off": [],
    "onboarded": true,
    "terminated": false,
    "terminations": []
  }
}
```
