---
permalink: /v1/current_user
title: Current User
layout: resource
---

# Current User

## Get information about the current user

> The self is a relation which relates itself to its own self, or it is that in the relation that the relation relates itself to its own self; the self is not the relation but that the relation relates itself to its own self.
>
> -Søren Kierkegaard

**HTTP Method**: `GET`

**Endpoint**: `/api/v1/me`

**Returns**: Information pertaining to the currently authenticated user.

#### Sample Response Body:

{% highlight javascript %}
    {
      "email" : "chris@zenpayroll.com",
      "roles" : {
        "payroll_admin" : {
          "company_ids" : [2357111317192329]
        }
      }
    }
{% endhighlight %}

| Field                     | Description
| :----------               |:-------------
| `email`                   | email address for the authenticated user.
| `roles`                   | information for each of the current user's permissions.
| `company_ids`             | array of company ids for which the current user has admin privileges. Users (most notably accountants) can have priviliges with multiple companies.