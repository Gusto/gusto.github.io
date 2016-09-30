---
permalink: v1/companies
title: Companies
layout: sidebar
---

# Companies

## Get Company Information

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id`

**Returns**: Get information about a particular company

{% highlight javascript %}
    {
      "id" : 2357111317192329,
      "name" : "Ye Olde Wig Shoppe",
      "trade_name" : "Fezziwig's",
      "locations" : [
        {
          "id" : 3141592653589793,
          "street_1" : "450 Serra Mall",
          "street_2" : "Department of Philosophy",
          "city" : "Stanford",
          "state" : "CA",
          "zip" : "94305"
        },
        {
          "id" : 2718281828459045,
          "street_1" : "314 Moses Hall #2390",
          "street_2" : "University of California",
          "city" : "Berkeley",
          "state" : "CA",
          "zip" : "94720"
        }
      ],
      "compensations" : {
        "hourly" : [
          {
            "name" : "Regular Hours",
            "multiple" : 1
          },
          {
            "name" : "Overtime",
            "multiple" : 1.5
          },
          {
            "name" : "Double Overtime",
            "multiple" : 2
          }
        ],
        "fixed" : [
          {
            "name" : "Bonus"
          },
          {
            "name" : "Commission"
          }
        ],
        "paid_time_off" : [
          {
            "name" : "Vacation Hours"
          },
          {
            "name" : "Sick Hours"
          }
        ]
      }
    }
{% endhighlight %}

| Field                     | Description
| :----------               |:-------------
| `id`                      | the unique identifier of this company in the Gusto system.
| `name`                    | name of this company.
| `trade_name`              | trade name of this company. This is an optional field.
| `locations`               | array of addresses for all known locations of this company.
| `id`                      | the unique identifier of this location in the Gusto system.
| `street_1`                | first line of this address' street.
| `street_2`                | second line of this address' street.
| `city`                    | name of address' city.
| `state`                   | two letter state abbreviation.
| `zip`                     | five digit zipcode. Returned as a string to maintain leading zeros.
| `compensations`           | all available company-wide compensations. The above compensations are the default, built-in compensations.
| `hourly`                  | available hourly compensations
| `name`                    | name of the compensation
| `multiple`                | amount multiplied by the base rate of a given job to calculate total compensation per hour worked. For example, if an employee at this company makes $17.00/hour as Kindergarten Cop and works 10 hours of Overtime (which has a multiple of 1.5), he would expect receive $150.
| `fixed`                   | available fixed compensations
| `name`                    | name of the compensation
| `paid_time_off`           | available types of paid time off
| `name`                    | name of the time off
