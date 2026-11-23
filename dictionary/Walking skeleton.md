---
description: A minimal end-to-end implementation that connects all main components and can be deployed before features are built.
---

A walking skeleton is a minimal implementation of a system that performs one small function end to end through all its main architectural components. Alistair Cockburn described the term. For an online shop, it might be a page that submits a hard-coded order through the API and a queue to a database, deployed by the real pipeline to a real environment.

It addresses integration problems that surface late. Teams build the frontend, API and data layer separately for months, each passing its own tests, and then discover during integration that authentication, message formats or deployment do not fit together. A walking skeleton forces those connections to work in the first days, when changing them is inexpensive.

To build one, pick the thinnest feature that touches each main component. Stub the business logic but keep the connections real: network calls, database access, configuration, deployment and monitoring. Run it in a production-like environment, then add features by thickening it, keeping the system runnable throughout.

| Technique              | Purpose                                    | Kept afterward?                 |
| ---------------------- | ------------------------------------------ | ------------------------------- |
| Walking skeleton       | Prove the architecture connects end to end | Yes, it grows into the product  |
| Prototype              | Answer a design or usability question      | Usually discarded               |
| Spike                  | Investigate one technical unknown          | Code discarded, learning kept   |
| Minimum viable product | Test whether users want the product        | Yes, and it provides user value |

The skeleton is not expected to be useful to users. It provides evidence that the chosen structure works, a deployment path from the start, and a shared running system for parallel teams to integrate against. It is a practical first step in an [evolutionary architecture](./Evolutionary%20architecture.md).

It helps less for a small change inside an established system, where the structure and pipeline already exist. Keep it thin. Adding real features before all components connect, or building abstractions for future needs, turns it into ordinary development and invites [speculative generality](./Speculative%20generality.md).

_Usage:_

"Every team is green on its own, but nothing has run together yet."

"Stop adding features. Get one hard-coded order through the whole stack and deployed this week."
