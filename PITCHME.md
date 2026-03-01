---
  marp: true
lang: en-US
title: Marp CLI example
description: Hosting Marp slide deck on the web
theme: uncover
transition: fade
paginate: true
_paginate: false
---

![bg opacity](./assets/gradient.jpg)

# <!--fit--> Er dette ein tittel ?

Our concern is related to large organizations where there is one organizational identifier, and operating many different digital services relying on the EUDI wallet

These services will be run by different product teams internally. 
Some services will be run by intermediaries (typically saas vendors)


We want isolation and data minimization between those services. This can be achieved by :

individual WRPAC to each service (but all of them will have the same organizational identifier)
individual WRPRC to each service (for sure, those services wil have different intended use)


The problem is now: what if one of those services is compromised - do we have mechanisms to limit the damage ?

our view: no.
an attacker at at compromised service can use his WRPAC to construct an over-reaching VP-request, asking for more personal data than its WRPRC allows, by not including the WRPRC in the request. 
Wallet would the look up the Registrar API using the organizational identifier
Register would return ALL intended uses for ALL services for this organization
User would not be prompted that this service is now asking for more personal data than is is allowed for.
