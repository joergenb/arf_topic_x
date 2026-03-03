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

- Services run by different product teams internally. 
- Some services will be run by intermediaries (typically saas vendors)

---

These organizations (and we) want isolation and data minimization between those services. This can be achieved by :

- Each service has its own WRP registration  (wrp-instance ?)
- Individual WRPAC to each service (but all of them will have the same organizational identifier)
- Individual WRPRC to each service (for sure, those services wil have different intended use)

Internal "plumbing" & Governance function at the org. distributes certificates.

--- 

Challenge: what if one of those services is compromised - do we have mechanisms to limit the blast radius ?

An attacker at at compromised service can use his WRPAC to construct an over-asking VP-request, asking for more personal data than its WRPRC allows, by **not** including the WRPRC in the request. 

1. Wallet would then look up the Registrar API using the organizational identifier (and possible the forged `intendedUseIdentifier`)
1. Register would return ALL intended uses for ALL services for this organization
1. User would not be prompted that this service is now asking for more personal data than is is allowed for.

---

## Countermeasures

1. A specific WRPAC must be bound to a specific IntendedUse (not the other way around)
  - 


2. National reguirements for Norwegian Wallets:
  - return error with missing WRPRC from Norwegian RP


WRPAC needs to point to a specific IntentedUse
- 
- Don't deploy the Registrar API
