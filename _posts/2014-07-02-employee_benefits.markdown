---
permalink: v1/employee_benefits
layout: resource
title: Employee Benefits
---

# Employee Benefits

Employee benefits represent an <a href="/v1/employees">employee</a> enrolled in a particular <a href="/v1/company_benefits">company benefit</a>. It includes information specific to that employee's enrollment.

## Attributes

| Attribute                     | Type              | Read-Only | Optional | Default | Description
| :----------                   |:-------------     |:---------:|:--------:|:--------|:-------------
| `id`                          | Integer           |     X     |          |         | the unique identifier of this employee benefit
| `version`                     | String            |     X     |          |         | version of this object. See <a href="/v1/considerations/versioning/">the versioning documentation</a> for a more in depth explaination of versions
| `employee_id`                 | Integer           |     X     |          |         | id for the employee to which this employee benefit belongs
| `company_benefit_id`                 | Integer           |     X     |          |         | id for the company benefit to which this employee benefit belongs
| `active`                      |  Boolean          |           |     X    | true    | whether or not this employee benefit is currently active
| `employee_deduction` | String | | X | '0.00' | the amount to be deducted, per pay period, from the employee's pay.
| `employee_deduction_annual_maximum` | String | | X | null | the maximum employee deduction per year. A null amount signifies no limit.
| `company_contribution` | String | | X | '0.00' | the amount to be paid, per pay period, from by the company
| `company_contribution_annual_maximum` | String | | X | null | the maximum company contribution per year. A null amount signifies no limit.
| `limit_option` | String | | X | null | certain benefits have particular options that need to be set to determine their limit option. For HSA, this should be either 'Family' or 'Individual' and for Dependent Care FSA this should be either 'Joint Filing or Single' or 'Married and Filing Separately'.
| `deduct_as_percentage` | Boolean | | X | false | if true, the employee_deduction amount will be treated as a percentage to be deducted from each payroll
| `contribute_as_percentage` | Boolean | | X | false | if true, the company_contribution amount will be treated as a percentage to be deducted from each payroll
| `catch_up` | Boolean | | X | | if true, the employee should use a benefit's special 'catch up' rate. Currently only the Roth 401k and 401k use this value for employees over 50.
| `coverage_amount` | String | | X | null | the amount that the employee is insured for (only applicable for group term life benefit)

## Get employee benefits for an employee

**HTTP Method**: `GET`

**Endpoint**: `/v1/employees/:employee_id/employee_benefits`

**Returns**: Array of all employee benefits for this employee

#### Sample Response Body:


```javascript
  [
    {
      "id": 1363316536327004,
      "version": '09j3d29jqdpj92109j9j2d90dq',
      "employee_id": 908123091820398,
      "company_benefit_id": 290384923980230,
      "active": true,
      "employee_deduction": '100.00',
      "company_contribution": '100.00',
      "employee_deduction_annual_maximum": '200.00',
      "company_contribution_annual_maximum": '200.00',
      "limit_option": null,
      "deduct_as_percentage": true,
      "contribute_as_percentage": true,
      "catch_up": false,
      "coverage_amount": null
    }
  ]
```

## Get a single employee benefit

**HTTP Method**: `GET`

**Endpoint**: `/v1/employee_benefits/:employee_benefit_id`

**Returns**: Single employee benefit representation

#### Sample Response Body:

```javascript
  {
    "id": 1363316536327004,
    "version": '09j3d29jqdpj92109j9j2d90dq',
    "employee_id": 908123091820398,
    "company_benefit_id": 290384923980230,
    "active": true,
    "employee_deduction": '100.00',
    "company_contribution": '100.00',
    "employee_deduction_annual_maximum": '200.00',
    "company_contribution_annual_maximum": '200.00',
    "limit_option": null,
    "deduct_as_percentage": true,
    "contribute_as_percentage": true,
    "catch_up": false,
    "coverage_amount": null
  }
```

## Update an employee benefit

**HTTP Method**: `PUT`

**Endpoint**: `/v1/employee_benefits/:employee_benefit_id`

**Returns**: Updated employee benefit or errors which prevent update

#### Sample Request Body:

```javascript
  {
    "version": '09j3d29jqdpj92109j9j2d90dq',
    "employee_deduction": '250.00'
  }
```

## Create an employee benefit

**HTTP Method**: `POST`

**Endpoint**: `/v1/employees/:employee_id/employee_benefits`

**Returns**: New employee benefit or errors which prevented creation

#### Sample Request Body:

```javascript
  {
    "company_benefit_id": 290384923980230,
    "active": true,
    "employee_deduction": '100.00',
    "company_contribution": '100.00'
  }
```

## Delete an employee benefit

**HTTP Method**: `DELETE`

**Endpoint**: `/v1/employee_benefits/:employee_benefit_id`

**Returns**: HTTP Status Code 204 (No Content) or errors which prevented destruction
