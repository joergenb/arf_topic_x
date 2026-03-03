---
marp: true
lang: en-US
title: "X: Registration of large organizations."
description: asdf
theme: default
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

- We assume an internal "plumbing" & Governance function at the org. which distributes certificates.

Based on security principles applied in our national Oauth2 infrastructure for datasharing.

<!-- We think of an RP as defined in the OpenID world - an oauth2 client / software system. Not an organisation -->

---

**Challenge 1:** Can we have multiple WRP registrations with the same identifier ?

ARF 6.6.3.2: 
> A) The Relying Party registered itself as described in Section 6.4.2 and obtained an access certificate for each of its Relying Party Instances.

but TS5-api:

> GET /wrp?identifier=someIdentifier   => *an array of matching WalletRelyingParty objects*
> GET /wrp/{identifier}  => *requesting a singular WalletRelyingParty object [...] that matches the identifier*

Seems not ?


--- 

**Challenge 2**: what if one of those services is compromised - do we have mechanisms to limit the blast radius ?

An attacker at a compromised service can use the WRPAC to construct an over-asking VP-request, asking for more personal data than its WRPRC allows, by **not** including the WRPRC in the request. 

1. Wallet would then look up the Registrar API using the organizational identifier
1. Register would return ALL intended uses for ALL services for this organization 
1. User would not be prompted that this service is now asking for more personal data than is is allowed for.

= WRPAC become a "universal key" for the organization.

<!-- A leaked WRPAC will be similar. VP-reqests will not be detected by Governace nor Registrar. 
-->


---

### Countermeasures

1. Demand national reguirements for Norwegian Wallets:

    - return error if WRPRC is missing (for a Norwegian WRPAC)
    - won't protect foreign users

2. Don't deploy the Registrar API

3. Standardize some mechanism binding a WRPAC to a specific IntendedUse
        - `x509_hash` from WRPAC as `client_id` in the WRPRC ?
        - allow `intendedUseIdentifier` into WRPAC ?

4. Make WRPRC mandatory

5. Considered using a composite identifier for each WRP-instance (business register id + "client_id")
        - probably breaks EU-ID syntax and other side-effects

