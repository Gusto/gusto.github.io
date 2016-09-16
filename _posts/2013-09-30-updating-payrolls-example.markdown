---
permalink: v1/examples/updating-payrolls
layout: resource
title: Updating Payrolls Example
---

# Updating Payrolls

## Getting Started

Payrolls can contain an overwhelming amount of information, but the basics of updating information should be a pain-free process.

Here we'll walk through updating the payroll information for one employee and how to handle conflicts.

We'll be using Ruby, with inefficient code, but the purpose of this example is to outline the flow rather than provide a production-ready implementation.

These examples will assume an <a href="/v1/examples/authentication">authenticated</a> application and will leave out the `access_token` parameter for clarity.

### Get Unprocessed Payroll

Let's say we have information for the regular hours of Patricia Churchland from January 01, 2014 through January 20, 2014:

```ruby
  work_data = [
    { date: '2014-01-02', hours: 8 },
    { date: '2014-01-03', hours: 8 },
    { date: '2014-01-06', hours: 8 },
    { date: '2014-01-07', hours: 8 },
    { date: '2014-01-08', hours: 8 },
    { date: '2014-01-09', hours: 8 },
    { date: '2014-01-10', hours: 8 },
    { date: '2014-01-13', hours: 8 },
    { date: '2014-01-14', hours: 8 },
    { date: '2014-01-15', hours: 8 },
    { date: '2014-01-16', hours: 8 },
    { date: '2014-01-17', hours: 8 },
    { date: '2014-01-20', hours: 8 }
  ]
```

 First we'll request the unprocessed payrolls for that time-period:

```
  GET https://api.gusto.com/v1/companies/94158/payrolls?processed=false&start_date=2014-01-01&end_date=2014-01-20
```

After deserializing the JSON response, we'll have an array of payroll objects:

```ruby
json_response = [
  {
    "version" => "6a46821b9249c9e30e66f39d61c209a2",
    "payroll_deadline" => "2014-01-18",
    "processed" => false,
    "pay_period" => {
      "start_date" => "2014-01-01",
      "end_date" => "2014-01-15",
      "pay_schedule_id" => 7757500908984137
    },
    "employee_compensations" => [
      {
        "employee_id" => 1123581321345589,
        "fixed_compensations" => [
          {
            "name" => "Bonus",
            "amount" => "0.00",
            "job_id" => 1
          },
          {
            "name" => "Commission",
            "amount" => "0.00",
            "job_id" => 1
          },
          {
            "name" => "Reimbursement",
            "amount" => "0.00",
            "job_id" => 1
          }
        ],
        "hourly_compensations" => [
          {
            "name" => "Regular Hours",
            "hours" => "0.000",
            "job_id" => 1,
            "compensation_multiplier" => 1
          }
        ],
        "paid_time_off" => []
      }
    ]
  },
  {
    "version" => "fb38ac6fdebea9646c4ac2e50ad27a21",
    "payroll_deadline" => "2014-02-03",
    "processed" => false,
    "pay_period" => {
      "start_date" => "2014-01-16",
      "end_date" => "2014-01-31",
      "pay_schedule_id" => 7757500908984137
    },
    "employee_compensations" => [
      {
        "employee_id" => 1123581321345589,
        "fixed_compensations" => [
          {
            "name" => "Bonus",
            "amount" => "0.00",
            "job_id" => 1
          },
          {
            "name" => "Commission",
            "amount" => "0.00",
            "job_id" => 1
          },
          {
           "name" => "Reimbursement",
           "amount" => "0.00",
           "job_id" => 1
          }
        ],
        "hourly_compensations" => [
          {
            "name" => "Regular Hours",
            "hours" => "10.000",
            "job_id" => 1,
            "compensation_multiplier" => 1
          }
        ],
        "paid_time_off" => []
      }
    ]
  }
]

```

This company seems to be on a semi-monthly pay schedule, paying their employees on the 15th and end of the month. We've already <a href="/v1/examples/syncing-employees">sync'd employees</a> and know that we are looking for `employee_id` 1123581321345589.

Looks like she is eligible for two types of fixed compensations, one type of hourly compensation, and no PTO.

Now we need to match up the totals from our data with the pay period it fits in. Because all of our dates are formatted according to [RFC-3339](http://tools.ietf.org/html/rfc3339#section-5.1), we can take advantage of simple string comparisions.


```ruby

# For each of the returned payrolls,
# group all work data that occured during
# that pay period

hourly_data_grouped_by_pay_period = json_response.reduce([]) do |grouped_data, payroll_json|
  start_date = payroll_json["pay_period"]["start_date"]
  end_date = payroll_json["pay_period"]["end_date"]
  grouped_data << work_data.select do |hourly_data|
    hourly_data[:date] >= start_date && hourly_data[:date] <= end_date
  end
end

# Sum each group to just get the hours worked
# during that pay period

hourly_totals = hourly_data_grouped_by_pay_period.map do |hourly_data|
  hourly_data.reduce(0) do |total_hours_worked, hourly_datum|
    total_hours_worked + hourly_datum[:hours]
  end
end

# hourly_totals = [ 80, 24 ]

```

### Building the Response

Now we need to build up the information to send to the Update Payrolls endpoint. All that is required is the version and the compensation information.

```ruby
updated_payroll_data = json_response.map.with_index do |payroll_json, index|
  # Find the compensation for Patricia Churchland
  churchland_compensation = payroll_json["employee_compensations"].detect { |compensation_json| compensation_json["employee_id"] == employee_id }

  # Find the 'Regular Hours' hourly compensation
  regular_hours_compensation = churchland_compensation["hourly_compensations"].detect { |hourly_compensation| hourly_compensation["name"] == 'Regular Hours' }

  # Update it to add our ours to the existing ones
  regular_hours_compensation["hours"] = regular_hours_compensation["hours"].to_d + hourly_totals[index]

  {
    "version" => payroll_json["version"],
    "employee_compensations" => [
      {
        "employee_id" => employee_id,
        "hourly_compensations" => [ regular_hours_compensation ]
      }
    ]
  }
end
```

Obviously our implementation would have to adapt if we were updating multiple employees simultaneously, or wanted to include multiple types of compensation, but that is the basic flow.

At this point, our JSON structure should look something like this:

```ruby
[
  {
    "version" => "6a46821b9249c9e30e66f39d61c209a2",
    "employee_compensations" => [
      {
        "employee_id" => 1123581321345589,
        "hourly_compensations" => [
          {
            "name" => "Regular Hours",
            "hours" => 80.0,
            "job_id" => 1,
            "compensation_multiplier" => 1
          }
        ]
      }
    ]
  },
  {
    "version" => "fb38ac6fdebea9646c4ac2e50ad27a21",
    "employee_compensations" => [
      {
        "employee_id" => 1123581321345589,
        "hourly_compensations" => [
          {
            "name" => "Regular Hours",
            "hours" => 34.0,
            "job_id" => 1,
            "compensation_multiplier" => 1
          }
        ]
      }
    ]
  }
]
```
Note that we had recorded 24 hours worked for the second pay period, but the above shows 34.0 hours worked. Unless you are certain that you want to overwrite the data returned via the API, you should only add to it. Making a request with 24.0 hours for the January 16-31 pay period would overwrite the existing 10 hours that are already in our system.

Now, for each payroll, we can send a PUT request to `https://api.gusto.com/v1/companies/94158/payrolls/:start_date/:end_date` (where start_date and end_date are for that payroll.) If everything goes well, we'll get response with a 200 OK status. But what if things have changed since we last pulled data from Gusto?

### Conflicts

If information has changed since your last pull of information from Gusto, you will receive a 409 Conflict response code.

This means that you will need to refetch the payroll data for that pay period and resubmit it. If, for example, the January 16-31 payroll has been updated, we can fetch it with a call to:

```
  GET https://api.gusto.com/v1/companies/94158/payrolls?processed=false&start_date=2014-01-16&end_date=2014-01-31
```

This should only return that one payroll and we can recompute the data specifically for that pay period. Do not simply copy over the new `version` and resubmit, as you'll likely be overwriting information that the user, an internal Gusto process, or another 3rd party application. This can lead to incorrect pay, miscalculated taxes, and upset users.
