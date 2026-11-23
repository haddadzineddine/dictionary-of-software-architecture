---
description: A single, simpler interface over a complicated subsystem, so callers do not need to coordinate its parts.
---

The facade pattern provides one simplified interface to a subsystem made of several classes or services. It is a structural pattern from the Gang of Four book (1994). The facade knows which parts to call and in what order, and callers use a small set of operations instead of coordinating those parts themselves.

```typescript
class CheckoutFacade {
  constructor(
    private inventory: Inventory,
    private payments: Payments,
    private shipping: Shipping,
    private email: Email,
  ) {}

  async placeOrder(order: Order) {
    await this.inventory.reserve(order.items);
    const payment = await this.payments.charge(order.total, order.customerId);
    const label = await this.shipping.createLabel(order.address);
    await this.email.sendConfirmation(order.customerId, payment.id, label.tracking);
  }
}
```

The pattern addresses workflows that every caller must reassemble. When the web handler, an admin script and a background job each call the same four services in sequence, they drift apart. One forgets to reserve stock, or sends the email before charging, and the resulting bug appears only through that entry point. A facade puts the sequence in one place and reduces [coupling](./Coupling.md) between callers and the subsystem's internals. A well-designed facade resembles a [deep module](./Deep%20module.md): a small interface in front of substantial behaviour.

A facade does not usually prevent direct access to the subsystem. Callers with an unusual need can still reach the underlying classes. If isolation is required, enforce it through module boundaries.

The main risk is growth. A facade that collects every operation in a domain becomes a [god object](./God%20object.md) that changes for every feature. Split it by use case when its methods stop relating to one another. A facade that only forwards each call to one method adds a layer with no benefit.

It is often confused with two related patterns:

| Pattern                             | Wraps                | Purpose                                 |
| ----------------------------------- | -------------------- | --------------------------------------- |
| Facade                              | Several objects      | Simplify use of a subsystem             |
| [Adapter](./Adapter%20pattern.md)   | Usually one object   | Convert to an expected interface        |
| [Mediator](./Mediator%20pattern.md) | Several peer objects | Coordinate peers, which talk through it |

A mediator also differs in direction. Subsystem classes do not know a facade exists, while colleagues actively send messages to their mediator.

A [service layer](./Service%20layer.md) often plays the facade role for an application's domain logic.

_Usage:_

"The admin tool created an order without reserving stock."

"It calls the services by hand. Route it through the checkout facade like the API does."
