---
permalink: v1/examples/syncing-employees
layout: layout_examples
title: Syncing Employees Example
---

# Syncing Employees

## Are We Talking About The Same People?

You have successfully <a href="/v1/examples/authentication">integrated with OAuth</a>, gotten back the authenticated
companies for the <a href="/v1/current_user">current user</a>, and fetched the
<a href="/v1/companies">company information</a>.

Now you have the JSON representation of 20 employees and need to map them to the employees in your database.

Naturally, the approach you'll choose will depend on the information you have available. Here are some suggestions for
matching up the employees in your database with the ones in ours. We recommend persisting the unique `id` attribute
that is returned by the Api, rather than redoing the match at the beginning of a pay period.

### Email Addresses

We provided email addresses with employee information specifically for matching employees between systems. For just
under 75% companies on Gusto, every single employee has an email address available.

This assumes that employees provide the same email address to both systems, but for work applications this is by far
the norm.

### Date of Birth

Almost 98% of employees in the Gusto system have birthdays associated with them. Of those that do, ~81% have a
unique birthday (comprised of year, month, and day).

Be careful when only comparing month and day, as it takes
[only 57 people](http://en.wikipedia.org/wiki/Birthday_problem) to achieve a 99% probability of collision.

### Full Name

First and last name are required for employees in the Gusto system. Additionally, ~55% provide middle initials.
If you can find an exact match based on full-name, then you're finished.

Typos do happen, in which case checking the [Hamming Distance](http://en.wikipedia.org/wiki/Hamming_distance) can be
helpful. If you have one unmatched set of employees with a Hamming Distance of 1, for example, it is pretty likely that
they are the same person.
