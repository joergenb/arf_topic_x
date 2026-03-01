---
  marp: true
lang: en-US
title: X: Registration of large organizations.
description: asdf
theme: gaia
transition: fade
paginate: true
_paginate: false
---

![bg opacity](./assets/gradient.jpg)

# <!--fit--> Topic X - registration: large organizations

Our concern is related to large organizations having one organizational identifier, and operating many different digital services relying on the EUDI wallet:

- These services will be run by different product teams internally. 
- Some services will be run by intermediaries (typically saas vendors)

---

They (and we) want isolation and data minimization between those services. This can be achieved by :

- individual WRPAC to each service (but all of them will have the same organizational identifier)
- individual WRPRC to each service (for sure, those services wil have different intended use)

Internal "plubming" at the org. distributes WRPAC and RC

--- 

The problem is now: what if one of those services is compromised - do we have mechanisms to limit the blast radius ?

An attacker at at compromised service can use his WRPAC to construct an over-reaching VP-request, asking for more personal data than its WRPRC allows, by **not** including the WRPRC in the request. 

1. Wallet would the look up the Registrar API using the organizational identifier
1. Register would return ALL intended uses for ALL services for this organization
1. User would not be prompted that this service is now asking for more personal data than is is allowed for.
