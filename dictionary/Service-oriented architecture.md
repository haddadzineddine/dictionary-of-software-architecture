---
description: Structuring enterprise systems as shared business services that communicate over the network through formal contracts.
---

Service-oriented architecture (SOA) structures a system as a set of business capabilities exposed as network services with formal contracts. It became widespread in large enterprises in the 2000s, often using SOAP, WSDL and an enterprise service bus (ESB).

It addressed capabilities duplicated across departmental applications. When sales, billing and support each keep their own customer record, an address change reaches one and the others go stale. SOA places a capability such as customer lookup behind one service, so applications reuse it rather than reimplement it.

A typical enterprise deployment has three parts. Business services expose capabilities through published contracts. The ESB routes messages, transforms formats and connects older systems. A governance group approves contracts and manages reuse.

The ESB is where many SOA programmes ran into trouble. Routing rules, data transformations and business logic accumulate in the bus, so a small change requires a ticket to the integration team and a shared release. The bus becomes a delivery bottleneck and a shared point of failure. Heavy reuse also increases [coupling](./Coupling.md), because a widely shared service cannot change without coordinating every consumer.

| Aspect            | Typical SOA               | Microservices                     |
| ----------------- | ------------------------- | --------------------------------- |
| Service scope     | Broad business capability | Narrow, independently deployable  |
| Data              | Often shared databases    | Owned per service                 |
| Integration logic | Central bus               | In the services, simple transport |
| Main goal         | Enterprise reuse          | Independent change and deployment |
| Governance        | Central                   | Mostly team-level                 |

Microservices are often described as a descendant of SOA, and the boundary between them is not sharp. SOA remains reasonable for integrating packaged products, such as ERP or CRM systems, that cannot be rewritten. Keep the bus limited to routing and protocol translation, and keep business rules inside the services. An [anti-corruption layer](./Anti-corruption%20layer.md) can protect newer code from a legacy contract.

_Usage:_

"Why does a new field on the customer API need the integration team?"

"The mapping lives in the ESB. Move it to the service and leave the bus doing routing only."
