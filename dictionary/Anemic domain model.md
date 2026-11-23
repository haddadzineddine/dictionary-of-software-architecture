---
description: A domain model whose objects hold only data while the business rules live in separate service classes.
---

An anemic [domain model](./Domain%20model.md) has objects that hold data while the business rules live in separate service classes. Martin Fowler described it as an anti-pattern in a 2003 article, because it carries the cost of a domain model, such as object mapping, without the benefit of keeping behaviour next to the data it governs.

```typescript
// Anemic: any caller can set an invalid status.
class AnemicOrder {
  status: "open" | "paid" | "shipped" = "open";
}

class OrderService {
  ship(order: AnemicOrder) {
    if (order.status !== "paid") throw new Error("Order is not paid");
    order.status = "shipped";
  }
}

// Rich: the rule lives with the state it protects.
class Order {
  #status: "open" | "paid" | "shipped" = "open";

  ship() {
    if (this.#status !== "paid") throw new Error("Order is not paid");
    this.#status = "shipped";
  }
}
```

The usual symptom is a rule enforced in one path and skipped in another. The checkout service checks that an order is paid before shipping, but a batch job or admin tool sets `status = "shipped"` directly, and unpaid orders go out. The [invariant](./Invariant.md) is unprotected because the object has no [encapsulation](./Encapsulation.md), so each new caller must know and repeat the rule.

To fix it, replace public setters with named methods such as `ship()` and move each rule onto the object whose data it checks. Keep a [domain service](./Domain%20service.md) for rules that span several objects and have no natural owner.

The pattern is not always a mistake. For an application that is mostly create, read, update and delete, plain data with a [transaction script](./Transaction%20script.md) is simpler and adequate. Functional codebases also separate data from functions by design, and can protect rules with immutable types and validated constructors. The anti-pattern applies when the domain has complex rules, the team maintains a model, and the rules are still scattered outside it.

An anemic object also differs from a [data transfer object](./Data%20transfer%20object.md). A data transfer object is meant to carry no behaviour, because its job is to move data across a boundary.

_Usage:_

"Support found shipped orders that were never paid."

"The admin tool sets `status` directly. Move the check into `order.ship()` and make the field private."
