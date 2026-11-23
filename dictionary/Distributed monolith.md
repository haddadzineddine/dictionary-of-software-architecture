---
description: Separately deployed services so tightly coupled that they must change, release or fail together.
---

A distributed monolith is a system split into separately deployed services that are so tightly coupled they must change, release or fail together. It carries the operational cost of microservices without their independence. The typical symptom is a release checklist: shipping one feature requires deploying six services in a fixed order, and one service being down stops the checkout flow.

The usual causes are specific and detectable:

| Cause                            | What happens                                  | Alternative                                 |
| -------------------------------- | --------------------------------------------- | ------------------------------------------- |
| Shared database                  | A schema change breaks other services         | Each service owns its data                  |
| Long synchronous call chains     | One slow service stalls every caller          | Use asynchronous messaging or merge them    |
| Shared domain library            | A version bump forces every service to deploy | Share only small, stable contracts          |
| Services split by technical layer | One feature touches every service            | Split by business capability                |
| Unversioned API changes          | Producer and consumers must deploy together   | Make backward-compatible changes            |

The problem usually starts with where the boundaries were drawn. A monolith split by database table or technical layer, instead of by [subdomain](./Subdomain.md), keeps its [coupling](./Coupling.md) and moves it onto the network. [Conway's law](./Conway's%20law.md) also applies: when service boundaries do not match team boundaries, routine changes need coordination across teams.

This outcome is usually worse than the monolith it replaced. Function calls become network calls, so the system gains latency, partial failure and harder debugging, while teams still cannot release independently. A [big ball of mud](./Big%20ball%20of%20mud.md) spread over a network is harder to change than one in a single process.

To diagnose it, use commit and deployment history to find services that always change together. Those services are candidates for merging. For the rest, remove shared tables and shorten synchronous call chains. A useful test is whether a team can deploy its service on an ordinary day without coordinating with another team. For a small organisation, a modular monolith is often a better destination than repairing many services.

_Usage:_

"Adding a field to the customer record needs deploys of six services, in order."

"Then they're one system. Let's start by merging the three that always change together."
