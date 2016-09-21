---
permalink: /v1/current_user
title: Current User
layout: layout_resources
---

# Current User

## Get information about the current user

**HTTP Method**: `GET`

**Endpoint**: `/v1/me`

**Returns**: Information pertaining to the currently authenticated user.

#### Sample Response Body:

{% highlight javascript %}
    {
      "email" : "chris@gusto.com",
      "roles" : {
        "payroll_admin" : {
          "companies" : [
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
            }
          ]
        }
      }
    }
{% endhighlight %}

| Field                     | Description
| :----------               |:-------------
| `email`                   | email address for the authenticated user.
| `roles`                   | information for each of the current user's permissions.
| `companies`               | array of basic company information for which the current user has admin privileges. Users (most notably accountants) can have priviliges with multiple companies.
