---
permalink: v1/paid_time_off
layout: sidebar
title: Paid Time Off
---

# Paid Time Off

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this paid time off
| `name`                        | String            |     X     |          |         | the name of this paid time off type. Currently only 'Vacation Hours' and 'Sick Hours' are supported
| `accrual_unit`                | String            |     X     |          |         | the unit this PTO is accrued in. Currently only 'Hour' is supported
| `accrual_period`              | String            |     X     |          |         | how often the pto accrues. Currently only 'Year' is supported
| `accrual_rate`                | String            |     X     |          |         | the rate at which accrual_unit is accrued per accrual_period
| `accrual_balance`             | String            |     X     |          |         | how many accrual_units have been accrued
| `maximum_accrual_balance`     | String            |     X     |          |         | the maximum accrual allowed. A null value signifies no maximum accrual
| `paid_at_termination`         | Boolean           |     X     |          |         | whether to pay out the accrual_balance to the employee upon their termaination
