---
description: The high-level structure of a system, covering its parts, their relationships and the decisions that are costly to change.
---

Software architecture is the structure of a software system: its major parts, how they relate, and the decisions that shape how it behaves and changes. In practice, the term covers decisions that are expensive to reverse, such as how the system is divided, where data lives and how components communicate.

There is no sharp line between architecture and design. A useful test is the cost of changing a decision later:

| Decision                             | Cost to reverse           | Usually considered |
| ------------------------------------ | ------------------------- | ------------------ |
| Name of a private function           | Minutes                   | Code detail        |
| Internal class structure of a module | Hours to days             | Design             |
| Public API contract                  | Weeks, involves consumers | Architecture       |
| Monolith or microservices            | Months                    | Architecture       |
| Primary data store                   | Months or longer          | Architecture       |

Architecture largely determines a system's [quality attributes](./Quality%20attribute.md), such as performance, availability, security and modifiability. A system can satisfy every functional requirement and still fail because its structure cannot meet them. One example is an application that works in a demo but cannot handle production traffic because every request joins across one shared database. Another is a small product change that requires edits in ten services, which points to misplaced boundaries and high [coupling](./Coupling.md).

Most architectural work is a series of [architectural trade-offs](./Architectural%20trade-off.md), where gaining one quality costs another. Because the reasoning is easy to lose, teams record significant choices in an [architecture decision record](./Architecture%20decision%20record.md).

Every codebase has an architecture, whether or not anyone designed it. Without attention, the structure tends toward a [big ball of mud](./Big%20ball%20of%20mud.md). It is also shaped by the organisation that builds it, as described by [Conway's law](./Conway's%20law.md). An architecture is judged against the system's goals and constraints, so a design suited to a large platform can be a poor choice for a three-person product.

_Usage:_

"Should this go to an architecture review, or can we decide in the PR?"

"How hard is it to undo? Renaming a class is fine. Changing the data store needs a review."
