---
description: Applying one familiar tool or pattern to every problem, including problems it does not fit.
---

A golden hammer is one familiar tool, technology or pattern applied to every problem, including problems it fits poorly. The name comes from the saying that if all you have is a hammer, everything looks like a nail. The symptoms include a search feature built on `LIKE '%term%'` that slows down with each new customer, a message queue used for simple function calls, and design meetings where the tool is chosen before anyone states the requirement.

The habit has understandable causes. The team knows the tool, has already invested in it and has seen it succeed. Hiring, vendor contracts and existing infrastructure all reinforce the choice, so the previous success feels like evidence for the next problem.

Standardising on a few tools is often the right decision, and it should not be confused with this anti-pattern. Every additional technology adds operational work, training and failure modes. Using an existing relational database for a modest job queue can be a sound choice. The difference lies in how the decision was made:

| Signal         | Reasonable standardisation                                | Golden hammer                     |
| -------------- | --------------------------------------------------------- | --------------------------------- |
| Why chosen     | Compared against the requirements                         | Chosen before requirements existed |
| Fit            | Meets the needed [quality attributes](./Quality%20attribute.md) | Needs growing workarounds         |
| Costs          | Known and accepted                                        | Not discussed                     |
| Exceptions     | Allowed with a written reason                             | Refused by default                |

To avoid it, write down the requirements before choosing a tool, including expected load and failure behaviour. Compare at least two options, one of which can be the current tool, and record the outcome in an [architecture decision record](./Architecture%20decision%20record.md). Revisit the choice when workarounds start to accumulate.

The same habit applies to design patterns. An engineer who has just learned the [strategy pattern](./Strategy%20pattern.md) may start using it for a single `if` statement. A golden hammer differs from [cargo cult programming](./Cargo%20cult%20programming.md), where a practice is copied without understanding it. The golden hammer user may understand the tool well and still apply it too widely.

_Usage:_

"Search takes nine seconds now. Should we add another index to the orders table?"

"That's the fourth workaround. Let's compare it against a dedicated search engine before adding a fifth."
