---
permalink: v1/partner_attributes
layout: sidebar
title: Partner Attributes
---

# Partner Attributes

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Description
| :----------                   |:-------------     |:---------:|:--------:|:-------------
| `grants_rev_share`            | Boolean           |     X     |    X     | true if you are receiving revenue sharing on behalf of this company
| `mapping`                     | Object            |     X     |    X     | how the company relates to an entity in your system
| `mapping:gusto:company_id`    | Integer           |     X     |    X     | unique identifier of this company in our system
| `mapping:partner:company_id`  | String            |     X     |    X     | unique identifier of this company in your system (optional; partner-dependent)

#### Sample Body:

```json
{
  "grants_rev_share": false,
  "mapping": {
    "partner": {
      "company_id": "a0c5e109-1a45-40e8-96c9-4fc83f8f08b6"
    },
    "gusto": {
      "company_id": 7389117231658670
    }
  }
}
```
