---
description: A small part of a domain model that two bounded contexts explicitly share and jointly own.
---

A shared kernel is a small part of a [domain model](./Domain%20model.md) that two bounded contexts explicitly share and jointly own. Neither team can change it without agreeing with the other. Eric Evans described it in Domain-Driven Design (2003) as one of the relationships recorded on a [context map](./Context%20map.md).

```typescript
// packages/billing-shipping-kernel/index.ts
export type OrderId = string & { readonly brand: "OrderId" };
export type Money = { cents: number; currency: "EUR" | "USD" };
```

The pattern addresses concepts that must stay identical on both sides. If billing and shipping each define `Money` or `OrderId` and the definitions diverge, values passed between them can be silently misread. Sharing a small package keeps the definition in one place, and the compiler catches disagreements.

The cost is [coupling](./Coupling.md) between the two teams. Every change requires coordination, and both contexts must build and test against it before it merges. The usual failure is growth. A package named `common` starts with two types and collects customer logic because that is convenient, until a change for one team breaks another team's deployment. At that stage, teams wait on each other's releases, which is one route to a [distributed monolith](./Distributed%20monolith.md).

| Relationship                                          | Who owns the model | Coordination | Use when                                |
| ----------------------------------------------------- | ------------------ | ------------ | --------------------------------------- |
| Shared kernel                                         | Both teams jointly | High         | Teams work closely, concept is identical |
| Customer-supplier                                     | Upstream team      | Medium       | One team depends on another             |
| [Anti-corruption layer](./Anti-corruption%20layer.md) | Each side          | Low          | The models differ                       |
| Separate copies                                       | Each side          | None         | The concepts may diverge                |

A shared kernel differs from a general utility library. A utility library has no domain meaning and holds things like string helpers and date formatting. A shared kernel holds business concepts. It also differs from applying [DRY](./DRY.md) across contexts: two definitions that look alike may represent different business concepts, and merging them ties together things that should change independently.

Keep the kernel small, give it tests that both teams run in CI, and require a review from each team on changes. If the teams stop coordinating or move to different release cycles, dissolve it and have each context own its copy.

_Usage:_

"Shipping's change to `common` broke our billing deploy again."

"That package has become a shared kernel nobody agreed to. Cut it down to `Money` and `OrderId` and move the rest back."
