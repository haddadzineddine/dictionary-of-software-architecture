---
description: Organising business logic as one procedure per request, each handling its own validation, rules and persistence.
---

A transaction script is a single procedure that handles one request from start to finish. It validates input, applies the business rules, reads and writes the database, and returns a result. Martin Fowler named the pattern in Patterns of Enterprise Application Architecture (2002). An application built this way has roughly one script per use case, often a route handler or a function in a services file.

```typescript
async function cancelOrder(db: Db, orderId: string) {
  await db.transaction(async (tx) => {
    const order = await tx.orders.find(orderId);
    if (!order) throw new NotFound();
    if (order.status === "shipped") throw new Conflict("Already shipped");

    await tx.orders.update(orderId, { status: "cancelled" });
    await tx.refunds.insert({ orderId, amount: order.total });
  });
}
```

The pattern suits simple logic. Each use case reads top to bottom, there is little indirection, and a developer can find a feature by finding its endpoint. For CRUD applications, internal tools and integrations that mostly move data, it is often the appropriate design, and more structure would add cost without protecting any rule.

The cost appears when rules start to interact. The check that a shipped order cannot be cancelled gets copied into the refund script, the admin script and the bulk import. When the rule changes, one copy is missed, and support finds an order refunded after it shipped. Shared helper functions delay this problem, but no single place owns the rule.

At that point, consider moving the affected logic into a [domain model](./Domain%20model.md), where the object that holds the data also enforces its rules. The move can be gradual: extract one rule at a time and leave simple scripts alone.

| Question               | Transaction script            | Domain model                      |
| ---------------------- | ----------------------------- | --------------------------------- |
| Where do rules live?   | In each procedure             | On objects that own the data      |
| Best fit               | Simple, independent use cases | Rules shared across use cases     |
| Cost of starting       | Low                           | Higher                            |
| Failure as logic grows | Duplicated conditionals       | Over-modelling when rules are few |

A transaction script is often confused with an [anemic domain model](./Anemic%20domain%20model.md). Both keep logic in procedures, but the anemic version also maintains domain classes that carry no behaviour, paying for the structure without receiving its benefit.

_Usage:_

"Cancelling from the admin panel still refunds shipped orders."

"The check only exists in the customer-facing script. Move it onto `Order` so both paths use it."
