---
description: Delaying an irreversible decision until the point where waiting longer would remove an important option or raise its cost.
---

The last responsible moment is the point at which delaying a decision further would eliminate an important option or make the outcome significantly more expensive. Mary and Tom Poppendieck brought the term to software in _Lean Software Development_ (2003). The aim is to make consequential decisions with as much information as possible, while still making them in time.

It addresses decisions made early on guesses. A team picks a database, a message broker and a service split in week one, before it knows its access patterns, then spends a year working around choices made when it had the least information.

The opposite failure is waiting too long. If a team postpones choosing an identity provider until just before launch, the delay has effectively made the decision, and the remaining options are all rushed. Delay is useful only when the team uses the time to learn.

| Decision type           | Example                                       | Approach                                             |
| ----------------------- | --------------------------------------------- | ---------------------------------------------------- |
| Easily reversed         | Logging library                               | Decide now and move on                               |
| Costly but isolated     | Search engine behind an interface             | Defer, and keep it behind a clear boundary           |
| Costly and far-reaching | Tenancy model, public API, primary data store | Investigate early, decide when evidence is sufficient |
| Blocks other teams      | Shared event schema                           | Decide as soon as the dependency arises              |

To keep an option open, put the volatile choice behind an [abstraction](./Abstraction.md), build a [walking skeleton](./Walking%20skeleton.md) to learn which constraints are real, and identify the date by which each decision must be made. Deferral has its own cost: abstractions added to preserve options can become [speculative generality](./Speculative%20generality.md), so use them only where a change is plausible.

The idea is related to [YAGNI](./YAGNI.md), which concerns not building features until they are needed. The last responsible moment concerns when to commit to a decision. When that point arrives, decide and write the reasoning in an [architecture decision record](./Architecture%20decision%20record.md).

_Usage:_

"Should we choose the tenancy model now, or wait for the enterprise requirements?"

"We can wait until the first schema migration next month. After that, changing it gets expensive."
