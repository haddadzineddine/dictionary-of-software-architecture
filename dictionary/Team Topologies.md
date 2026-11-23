---
description: A model for organising software teams around flow, using four team types and three ways of interacting.
---

Team Topologies is a model for organising software teams around the flow of delivery, introduced by Matthew Skelton and Manuel Pais in their 2019 book of the same name. It defines four team types and three interaction modes, and treats team cognitive load as the main limit on what any team should own.

| Team type             | Purpose                                                            |
| --------------------- | ------------------------------------------------------------------ |
| Stream-aligned        | Delivers a flow of change for one product, service or user journey |
| Platform              | Provides internal services that reduce work for other teams        |
| Enabling              | Helps other teams acquire new skills, then moves on                |
| Complicated-subsystem | Owns a part that needs deep specialist knowledge                   |

| Interaction mode | Meaning                                 | Suited to                       |
| ---------------- | --------------------------------------- | ------------------------------- |
| Collaboration    | Two teams work closely for a period     | Discovering a new boundary      |
| X-as-a-Service   | One team consumes what another provides | Stable, well-defined boundaries |
| Facilitating     | One team coaches another                | Closing a skill gap             |

Cognitive load is the amount of information a team must hold to do its work. When one team owns a dozen services, their pipelines, on-call and a legacy system, each change means rediscovering how something works, and delivery slows. The remedy is to reduce what the team owns, by narrowing its scope or moving undifferentiated work to a platform.

Stream-aligned teams are the default, and the other three types exist to reduce their burden. A common failure is a platform that teams are forced to use and that needs a ticket for routine work. Run a platform as a product with internal customers.

The model builds on [Conway's law](./Conway's%20law.md), because team boundaries shape system boundaries, and it gives vocabulary for an [inverse Conway maneuver](./Inverse%20Conway%20maneuver.md). Interactions are expected to change, for example from collaboration while a boundary is explored to X-as-a-Service once it settles. Renaming existing teams without changing ownership or interactions has no effect.

_Usage:_

"Our team owns fourteen services and nobody understands all of them."

"That's too much cognitive load. Move the shared infrastructure to a platform team and narrow our scope."
