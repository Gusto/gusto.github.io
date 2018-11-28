---
permalink: v1/webhooks/locations
title: Locations Webhooks
layout: sidebar
---

# Locations Webhooks

## Get Location Webhook Notifications
[Webhooks Overview](/v1/webhooks/about)

**Resource**: `Company`

**Entity**: `Location` ([API Reference](/v1/locations))


**Event Types**:

- `location.created`

- `location.updated`

**Returns**: Get information about a particular location that was created or updated

```json
{
  "event_type": "location.created",
  "resource_type": "Company",
  "resource_id": 1402341716000,
  "entity_type": "Location",
  "entity_id": 1402342024000,
  "timestamp": 1533606328,
  "entity_attributes": {
    "id": 1402342024000,
    "version": "fe75bd065ff48b91c35fe8ff842f986c",
    "phone_number": "8009360383",
    "company_id": 1402341716000,
    "street_1": "21 Stillman Street",
    "street_2": "Apartment 6",
    "city": "San Francisco",
    "state": "CA",
    "zip": "94107",
    "country": "USA"
  }
}
```
