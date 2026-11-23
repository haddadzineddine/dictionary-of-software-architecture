---
description: A measurable property of a system, such as latency or availability, describing how well it works rather than what it does.
---

A quality attribute is a measurable property of a system that describes how well it performs its function, rather than what the function is. Examples include performance, availability, security, modifiability, scalability and testability. The term overlaps with non-functional requirement, and architects often prefer it because these properties drive structural decisions.

Unstated quality attributes are a frequent source of late surprises. A feature passes every test, ships, and then times out on the first busy day, because "it should be fast" was never turned into a number. A vague goal gives the team nothing to design for or verify.

To make an attribute usable, express it as a concrete scenario with a stimulus, a context and a measurable response:

| Attribute     | Example scenario                                                     |
| ------------- | -------------------------------------------------------------------- |
| Performance   | At 2,000 requests per second, 99% of checkouts finish within 400 ms  |
| Availability  | If one zone fails, service recovers within 60 seconds                |
| Modifiability | A new payment provider can be added in one module within a week      |
| Security      | After 5 failed logins in a minute, further attempts are blocked      |
| Testability   | The domain test suite runs without network access in under 2 minutes |

Quality attributes conflict. Replication improves availability but complicates consistency, encryption improves security but adds latency, and caching improves read performance but serves staler data. Because these are [architectural trade-offs](./Architectural%20trade-off.md), rank the attributes for the specific system rather than asking for all of them at maximum. An internal admin tool and a payment gateway should not have the same targets.

Once targets exist, check them continually. A [fitness function](./Fitness%20function.md), such as a latency threshold in a load test, turns a scenario into an automated check. For high-stakes systems, the [Architecture Tradeoff Analysis Method](./Architecture%20Tradeoff%20Analysis%20Method.md) evaluates a design formally against prioritised scenarios.

_Usage:_

"The requirement says the dashboard must be fast. What does that mean?"

"Ask for a number. If it's two seconds at p95 for 500 users, we can design and test for that."
