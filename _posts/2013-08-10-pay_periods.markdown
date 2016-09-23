---
permalink: v1/pay_periods
layout: sidebar
title: Pay Periods
---

# Pay Periods

## Frequency of Payment

> **Note**:
> Pay periods are the foundation of payroll. Compensation, time & attendance, taxes, and expense reports all rely on when they happened. To begin submitting information for a given payroll, we need to agree on the time period.

### Get Pay Periods for a Company

**HTTP Method**: `GET`

**Endpoint**: `/v1/companies/:company_id/pay_periods`

**Returns**: Array of all pay periods, past and current, for a company.

#### Sample Response Body:

{% highlight javascript %}
  [
    {
      "start_date" : "2013-02-01",
      "end_date" : "2013-02-15",
      "pay_schedule_id" : 7757500908984137,
      "payroll" : {
        "payroll_deadline" : "2013-02-18",
        "processed" : true,
      },
      "eligible_employees" : [
        {
          "employee_id" : 1123581321345589,
          "job_ids" : [1]
        },
        {
          "employee_id" : 1442333776109871,
          "job_ids" : [2]
        }
      ]
    }
  ]
{% endhighlight %}

| Field                     | Description
| :----------               |:-------------
| `start_date` & `end_date` | the range of the pay period. So any information you have from February 1, 2013 through February 15, 2013 (inclusive) should be applied to this pay period.
| `payroll`                 | meta information relative to the company's payroll for the requested pay period.
| `payroll_deadline`        | date by which payroll should be run for employees to be paid on time. This helps you plan in advance for submitting data. For example, if you are tracking time and attendance data, you should submit the cumulative hours for the tracked employees on, and preferably before, this date.
| `processed`               | whether or not this payroll has been successfully run. If it has, you should consider it 'frozen', as any attempts to update its data will be rejected. Note that passing the `payroll_deadline` does not guarantee that the payroll has been processed; running late payrolls is not uncommon.  Similarly, Gusto users may choose to run payroll before the `payroll_deadline`.
| `eligible_employees`      | array of all employees who are (or were) eligible during the given pay period.
| `id`                      | the unique identifier of this employee in the Gusto system.
| `job_ids`                 | unique ids of jobs worked (or eligible to be worked) by this employee during this pay period.

### Optional Parameters

This endpoint, by default, returns all pay periods for a given company. Companies can process payroll as often as every week, meaning there will be 53 pay periods per year. That's a lot of information, and more then you are likely to need, so we've included some optional parameters to scope things down.

  **Available options**: `start_date`, `end_date`

You may provide all, none, or any combination of them to scope the returned data. Here are some common use cases:

    GET /v1/companies/3337/pay_periods?start_date=2012-01-31
      => returns all pay periods from the one encompassing January 31, 2012 through the current pay period

    GET /v1/companies/3337/pay_periods?start_date=2012-01-31&end_date=2012-06-30
      => returns all pay periods from January 31, 2012 through June 30, 2012-01-31

