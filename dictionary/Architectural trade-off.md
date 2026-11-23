---
description: A design choice that improves one system quality at the expense of another, made deliberately for a given context.
---

An architectural trade-off is a design decision in which improving one property of a system reduces another. Most structural choices involve one: a design that improves [quality attributes](./Quality%20attribute.md) such as availability or scalability usually costs simplicity, consistency, latency or money.

| Choice                            | Gains                                 | Costs                                     |
| --------------------------------- | ------------------------------------- | ----------------------------------------- |
| Microservices over a monolith     | Independent deployment, team autonomy | Network failures, operational load        |
| Read replicas                     | Read capacity                         | Stale reads                               |
| Caching                           | Lower latency and load                | Invalidation complexity, stale data       |
| Asynchronous messaging            | Load smoothing, looser dependencies   | Eventual consistency, harder debugging    |
| Strong consistency across regions | Correct reads everywhere              | Higher write latency, outages in partitions |
| Shared library                    | Less duplication                      | [Coupling](./Coupling.md) between consumers |

Trade-offs that go unstated tend to surface later as surprises. A team adopts an event bus because it is considered good practice, then discovers months later that support cannot explain why an order's status differs between two screens. The cost was present from the day of the decision, but nobody named it or agreed it was acceptable.

To make a trade-off deliberately, start with the qualities the system needs most and rank them. List realistic options, including the simplest one, and state what each gives up. Prefer evidence from a prototype, load test or production data over general reputation. Then record the reasoning in an [architecture decision record](./Architecture%20decision%20record.md), including the conditions under which the decision should be revisited.

Context decides the answer. Eventual consistency may be acceptable for a social feed and unacceptable for account balances. Copying a design from a large technology company imports trade-offs chosen for that company's scale and team structure, which can become [cargo cult programming](./Cargo%20cult%20programming.md). For a reversible decision, choose quickly and adjust. For an expensive one, consider waiting until the [last responsible moment](./Last%20responsible%20moment.md).

_Usage:_

"Let's make this asynchronous. It'll be more scalable."

"It will, but users may see stale status. Is that acceptable for refunds?"
