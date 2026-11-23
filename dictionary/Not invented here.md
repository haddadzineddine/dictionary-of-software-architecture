---
description: Rejecting existing solutions and rebuilding them in-house, mainly because they came from outside the organisation.
---

Not invented here is the tendency to reject an existing solution and build an in-house replacement, mainly because the solution came from outside the team or organisation. It is recognisable in a company that maintains its own authentication library, date parser, job queue and CSS framework, each with bugs that open-source projects fixed years ago. The engineer who wrote each one has often left, and new hires have to learn tools that exist nowhere else.

Writing the first version is usually a small part of the cost. The team also takes on security patches, documentation, onboarding and edge cases in areas such as time zones, Unicode and cryptography. That effort comes out of work on an organisation's [core domain](./Core%20domain.md), the part of the business that sets it apart. Generic [subdomains](./Subdomain.md) such as email delivery or payments processing are usually better bought or adopted.

The decision depends on several factors:

| Factor             | Favours adopting                       | Favours building                       |
| ------------------ | -------------------------------------- | -------------------------------------- |
| Business relevance | Generic capability                     | Differentiates the product             |
| Fit                | Meets needs with small adaptations     | Requires heavy workarounds             |
| Risk area          | Security, cryptography, date handling  | Narrow, well-understood logic          |
| Project health     | Actively maintained                    | Abandoned or unmaintained              |
| Dependency size    | Proportionate to what you use          | Large package for one small function   |

The opposite failure is also a risk. Importing a large package for one function adds supply-chain exposure and upgrade work, and a few lines of well-understood code may be the better choice. Building can also be justified by licensing, latency or compliance requirements that no external option meets.

When adopting a dependency, limit how far it spreads. An [adapter](./Adapter%20pattern.md) or [anti-corruption layer](./Anti-corruption%20layer.md) keeps the vendor's types out of business code, so the dependency can be replaced later. Record the reasoning in an [architecture decision record](./Architecture%20decision%20record.md), including what would cause the team to revisit it.

_Usage:_

"Our date library has handled daylight saving wrongly again."

"We wrote it years ago and nobody owns it. Let's move to a maintained library behind one small wrapper."
