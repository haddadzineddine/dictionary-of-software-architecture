---
description: A translation boundary that stops an external or legacy system's model from spreading into a domain's own model.
---

An anti-corruption layer is a translation boundary that stops the model of an external or legacy system from spreading into a domain's own model. Code on the inside works only with its own concepts, and the layer converts to and from the foreign representation. Eric Evans described it in Domain-Driven Design (2003).

```typescript
type LegacyCustomer = { CUST_NO: string; STAT_CD: "A" | "S" | "X" };

const statuses = { A: "active", S: "suspended", X: "closed" } as const;

function toCustomer(raw: LegacyCustomer): Customer {
  return new Customer(CustomerId.of(raw.CUST_NO), statuses[raw.STAT_CD]);
}
```

The pattern addresses foreign concepts leaking into new code. A team rewrites a service, but because the data comes from a mainframe, the new classes contain fields like `STAT_CD`, the business logic branches on `"X"`, and every developer has to learn what the old codes mean. With a layer in place, the codes exist in one translation module, and the domain sees `suspended` and `closed`.

The layer usually combines a [facade](./Facade%20pattern.md) that simplifies the foreign API, [adapters](./Adapter%20pattern.md) that fit it to the interfaces the domain expects, and translators that convert data. It may also reconcile differences in behaviour, for example by combining three legacy calls into one domain operation.

| Option                     | Cost                         | Use when                                     |
| -------------------------- | ---------------------------- | -------------------------------------------- |
| Conform to upstream model  | Low now, [coupling](./Coupling.md) later | The upstream model is good or the area is generic |
| Thin [gateway](./Gateway%20pattern.md) | Low              | Stable API, few concepts cross the boundary  |
| Anti-corruption layer      | Higher, with ongoing mapping | The foreign model is poor and the domain matters |

The layer is a maintenance cost, so apply it where the model matters. Protecting a [core domain](./Core%20domain.md) from a legacy schema usually justifies the effort. Wrapping a payment provider used in one generic flow usually does not. It is also a common companion to the strangler fig approach, where it lets new code run beside a legacy system during a migration.

An anti-corruption layer differs from a single adapter. An adapter fits one interface to another, often with one-to-one calls. An anti-corruption layer protects a model, and can contain substantial translation logic and many adapters.

_Usage:_

"Why does the new billing code check `STAT_CD === "X"`?"

"It reads the legacy record directly. Add an anti-corruption layer that maps those codes to our `AccountStatus`."
