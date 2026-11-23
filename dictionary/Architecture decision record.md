---
description: A short document capturing one significant technical decision, its context and its consequences, stored with the code.
---

An architecture decision record (ADR) is a short document that captures one significant technical decision, the context that led to it and its consequences. Michael Nygard proposed the format in 2011. ADRs are usually numbered Markdown files stored in the repository, for example `docs/adr/0012-use-postgres-for-orders.md`.

ADRs address lost reasoning. A new engineer asks why orders go through a queue, nobody who made the choice is still on the team, and the group either reopens a settled debate or removes a constraint that existed for a reason. A record lets them read what was known at the time.

| Section      | Contents                                                  |
| ------------ | --------------------------------------------------------- |
| Title        | The decision, in a short phrase                           |
| Status       | Proposed, accepted, deprecated or superseded              |
| Context      | Forces and constraints at the time                        |
| Decision     | What the team will do                                     |
| Consequences | What becomes easier and harder, including costs accepted  |

```markdown
# 12. Use Postgres for orders

Status: Accepted

Context: Orders need multi-row transactions. The team already runs Postgres.

Decision: Store orders in Postgres rather than DynamoDB.

Consequences: Joins and transactions are simple. Write scaling is limited to one primary.
```

Treat accepted records as immutable. When a decision changes, write a new ADR that supersedes the old one, and change only the old record's status. The sequence then shows how the team's thinking developed.

Write an ADR for choices that are costly to reverse or that affect [quality attributes](./Quality%20attribute.md), such as data stores, integration styles and module boundaries. Do not write one for routine implementation choices, or the collection becomes noise. The Consequences section should name what was given up, because a later reader needs to know the [architectural trade-off](./Architectural%20trade-off.md) that was accepted. Keeping records in the repository lets them be reviewed in pull requests alongside the code they affect.

_Usage:_

"Why are we using a queue here instead of a direct call? Can I remove it?"

"Check ADR 31 first. It records the outage that led to it."
