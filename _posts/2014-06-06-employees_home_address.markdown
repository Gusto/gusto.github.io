---
permalink: v1/employee_home_address
layout: resource
title: Employee Home Address
---

# Employee's Home Address

The home address of an employee determines some tax information about them. Addresses are geocoded on create/update to ensure validity.

## Attributes

| Attribute                     | Type              | Read-Only | Description
| :----------                   |:-------------     |:---------:|:-------------
| `id`                          | Integer           |     X     | unique identifier of this address
| `version`                     | String            |     X     | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `employee_id`                 | Integer           |     X     | id of the employee to which this address belongs
| `street_1`                    | String            |           | first line of the address
| `street_2`                    | String            |           | second line of the address
| `city`                        | String            |           | city of the address
| `state`                       | String            |           | state of this address
| `zip`                         | String            |           | zipcode of this address
| `country`                     | String            |           | country for this address. Defaults to "USA"

## Get an employee's home address

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/employees/:employee_id/home_address`

**Returns**: Address object for an employee's home address

#### Sample Response Body:

```javascript
  {
    "id" : 1402342024000
    "version" : "fe75bd065ff48b91c35fe8ff842f986c",
    "employee_id" : 1402341716000,
    "street_1": "425 2nd Street",
    "street_2": "Suite 602",
    "city" : "San Francisco",
    "state" : "CA",
    "zip" : "94107",
    "country" : "USA"
  }
```

## Update an employee's home address

**HTTP Method**: `PUT`

**Endpoint**: `/api/v1/employees/:employee_id/home_address`

**Returns**: Updated address or errors which prevented update

#### Sample Request Body:

```javascript
  {
    "version" : "fe75bd065ff48b91c35fe8ff842f986c",
    "street_1": "300 3rd Street",
    "street_2": null,
    "city" : "San Francisco",
    "state" : "CA",
    "zip" : "94107"
  }
```
