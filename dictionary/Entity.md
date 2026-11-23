---
description: A domain object defined by a stable identity that persists as its attributes change.
---

An entity is a domain object defined by a stable identity and not by its attribute values. A customer who changes their name, email and address is still the same customer, because the identity persists through those changes. Eric Evans described entities in Domain-Driven Design (2003), alongside [value objects](./Value%20object.md), which have no identity.

```typescript
class Customer {
  constructor(readonly id: CustomerId, private email: Email) {}

  changeEmail(email: Email) {
    this.email = email;
  }

  equals(other: Customer) {
    return this.id === other.id;
  }
}
```

Identity determines equality. Two `Customer` objects with the same ID represent the same customer even if one has stale fields, and two customers named Sam Lee with different IDs are different people. A frequent bug comes from ignoring this: code compares objects with `===`, which checks the in-memory reference, so two loads of one customer appear unequal and a deduplication step keeps both. Comparing by ID fixes it, and an [identity map](./Identity%20map.md) can also ensure a single instance per session.

A good identity is generated once and never reused. Natural keys such as email addresses are risky because they change: a customer who updates their email either breaks every foreign key that references it or gets split into two records. Prefer a generated ID, and keep natural keys as unique attributes.

An entity has a lifecycle, and its methods should protect it. In place of public setters, expose operations such as `deactivate()` that check the [invariants](./Invariant.md) for that transition. An entity with only getters and setters, whose rules live elsewhere, is part of an [anemic domain model](./Anemic%20domain%20model.md).

The word has a narrower meaning in ORMs, where an entity is a class mapped to a table. A domain entity need not correspond to one table, and join tables and lookup rows are often not entities at all. To decide, ask whether the business tracks this thing individually over time. If two instances with the same values are interchangeable, model it as a value object. An entity may also sit inside an [aggregate](./Aggregate.md), which controls changes to it.

_Usage:_

"The merge script kept both copies of the same customer."

"It compared objects by reference. Compare by customer ID, since that is what makes them the same entity."
