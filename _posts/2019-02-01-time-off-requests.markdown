---
permalink: v1/time_off_requests
layout: sidebar
title: Time Off Requests
---

# Time Off Requests

## Get all Time Off Requests for a Company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/time_off_requests/`

**Returns**: Array of all time off requests, current and past, for a company

#### Sample Response Body:
```json
[
  {
    "id": "1",
    "status": "approved",
    "employee_note": "Vacation at Disney World!",
    "employer_note": "But Universal has Harry Potter World...",
    "days": {
      "2019-06-01": "4.000",
      "2019-06-02": "8.000",
      "2019-06-03": "8.000",
      "2019-06-03": "2.000"
    },
    "request_type": "vacation",
    "employee": {
      "id": "234567",
      "full_name": "Jessica Gusto"
    },
    "approver": {
      "id": "345678",
      "full_name": "Karen Gusto"
    },
    "initiator": {
      "id": "234567",
      "full_name": "Jessica Gusto"
    }
  },
  {
    "id": "2",
    "status": "pending",
    "employee_note": "Coming down with the flu",
    "employer_note": "",
    "days": {
      "2019-02-01": "8.000"
    },
    "request_type": "sick",
    "employee": {
      "id": "654321",
      "full_name": "James Gusto"
    },
   "approver": null,
   "initiator": {
     "id": "654321",
     "full_name": "James Gusto"
   }	    
 }
]
```

#### Optional Parameters
In order to reduce the number of time off requests returned in a single response, or to retrieve time off requests from a time period of interest, you may use the `start_date` and `end_date` parameters.

You may provide both or either parameters to scope the returned data. For example:

Return all time off requests where the request start date is equal to or after May 1, 2019 and the  request end date is equal to or before August 31, 2019:

=> `/v1/companies/:company_id/time_off_requests/start_date='2019-05-01'&end_date='2019-08-31'`

Return all time off requests where the request start date is equal to or after January 1, 2019:

=> `/v1/companies/:company_id/time_off_requests/start_date='2019-01-01'`

Return all time off requests where the request end date is equal to or before January 1, 2019:

=> `/v1/companies/:company_id/time_off_requests/end_date='2019-01-01'`

## Get a specific Time Off Request

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/time_off_requests/:time_off_request_id`

**Returns**: Details of a single time off request

#### Sample Response Body:
```json
[
  {
    "id": "1",
    "status": "approved",
    "employee_note": "Vacation at Disney World!",
    "employer_note": "But Universal has Harry Potter World...",
    "days": {
      "2019-06-01": "4.000",
      "2019-06-02": "8.000",
      "2019-06-03": "8.000",
      "2019-06-03": "2.000"
    },
    "request_type": "vacation",
    "employee": {
      "id": "234567",
      "full_name": "Jessica Gusto"
    },
    "approver": {
      "id": "345678",
      "full_name": "Karen Gusto"
    },
    "initiator": {
      "id": "234567",
      "full_name": "Jessica Gusto"
    }
  }
]
```

## Attributes

| Attribute       | Type      | Read-Only | Description
| :----------     |:-------   |:-------   |:-------------
| `id`            | Integer   |     X     | The unique identifier of this time off request in the Gusto system
| `status`        | String    |     X     | The status of the time off request (i.e. pending, approved, declined)
| `employee_note` | String    |     X     | A note about the time off request, from the employee to the employer.
| `employer_note` | String    |     X     | A note about the time off request, from the employer to the employee.
| `request_type`  | String    |     X     | The type of time off request, either vacation or sick.
| `days`          | Array     |     X     | An array that represents the days in the time off request. The keys of the array are the dates, formatted as a YYYY-MM-DD string. The values of the array are the number of hours requested off for each day, formatted as a string representation of a numeric decimal to the thousands place.
| `employee`      | Array     |     X     | An array containing the `id` and `full_name` of the employee the time off request is for.  
| `initiator`     | Array     |     X     | An array containing the `id` and `full_name` of the user who created the time off request. This value may be null.
| `approver`      | Array     |     X     | An array containing the `id` and `full_name` of the user who approved the time off request. This value will be null if the request has not been approved.
