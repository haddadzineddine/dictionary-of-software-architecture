---
description: A cluster of domain objects changed as one consistent unit through a single root object.
---

An aggregate is a cluster of domain objects that is treated as one unit for changes, with a single root [entity](./Entity.md) through which all modifications pass. An `Order` root might contain `OrderLine` objects, and code outside calls `order.addLine()` without ever editing a line directly. Eric Evans described the pattern in Domain-Driven Design (2003).

```typescript
class Order {
  private lines: OrderLine[] = [];

  constructor(
    readonly id: OrderId,
    readonly customerId: CustomerId,
    private limit: Money,
  ) {}

  addLine(product: ProductId, price: Money, quantity: number) {
    const line = new OrderLine(product, price, quantity);
    if (this.total().add(line.subtotal()).greaterThan(this.limit)) {
      throw new OrderLimitExceeded();
    }
    this.lines.push(line);
  }

  total() {
    return this.lines.reduce((sum, l) => sum.add(l.subtotal()), Money.zero("EUR"));
  }
}
```

The pattern protects rules that span several objects. Suppose an order may not exceed a credit limit. If two requests each insert a line, each can check the total, each can pass, and the order ends up over the limit. With an aggregate, the order's [invariants](./Invariant.md) are checked in one place, and a version number on the root detects the concurrent edit.

| Rule                                   | Reason                         |
| -------------------------------------- | ------------------------------ |
| Access children only through the root  | Nothing can bypass the rules   |
| Reference other aggregates by ID       | Keeps object graphs small      |
| Change one aggregate per transaction by default | Limits locking and contention |
| Load and save the aggregate as a whole | Rules see the complete state   |

Size is the main design decision. A common mistake is to model a `Customer` aggregate containing all orders, addresses and tickets because the nouns are related. Loading it pulls thousands of rows, and unrelated updates fail with version conflicts. Draw the boundary around what must be consistent immediately. Anything else can be updated afterwards, often in response to a [domain event](./Domain%20event.md).

An aggregate differs from an ORM relationship graph, which lets code navigate between objects and save each independently. It also differs from the [composite pattern](./Composite%20pattern.md), which treats a tree of objects uniformly and says nothing about transactional consistency. For data with no multi-object rules, a plain entity or a [transaction script](./Transaction%20script.md) is enough.

_Usage:_

"Two people edited the same order and it went over the credit limit."

"Lines are saved independently. Make `Order` the aggregate root and check the limit in `addLine`."
