---
description: A shared vocabulary that developers and domain experts use in conversation, documents and code.
---

A ubiquitous language is a shared vocabulary that developers and domain experts use for a business domain, in conversation, in documents and in the code itself. Eric Evans introduced the term in Domain-Driven Design (2003). If the business says a policy is "renewed", the code has a `renew()` method and not `updateStatus(3)`.

The practice addresses translation between business and engineering. When sales says "account" for a company, support says "account" for a login, and the code calls both `User`, every conversation needs interpretation, and a ticket can be built correctly against the wrong meaning. The mismatch is often found late, when a feature ships and the stakeholder says it is not what they asked for.

| Business says       | Code without a shared language | Code with one             |
| ------------------- | ------------------------------ | ------------------------- |
| Renew a policy      | `updateStatus(policy, 3)`      | `policy.renew()`          |
| Member has lapsed   | `user.flag === false`          | `member.hasLapsed()`      |
| Item is back-ordered | `item.qty < 0`                | `item.isBackOrdered()`    |

A ubiquitous language applies within one bounded context and is not a company-wide glossary. "Customer" can legitimately mean different things in billing and in shipping, and forcing one definition produces a bloated model that fits neither. A [context map](./Context%20map.md) records where meanings change and how terms translate between contexts.

Maintaining the language takes ongoing work. Keep a short glossary in the repository, using the words domain experts use. When a discussion changes the meaning of a term, rename the class, the method and the database column as part of the same work, or the code and the conversation drift apart. If a concept is hard to name, raise it with the experts as a modelling question, since the difficulty often means the concept is not yet understood.

The vocabulary feeds the [domain model](./Domain%20model.md), where each important term has a corresponding type or method. A developer reading the code and an expert describing the process should then be using the same words for the same things.

_Usage:_

"Is a member the person paying or the person on the plan?"

"Ask support, then use their word everywhere. Right now the code calls both `user`."
