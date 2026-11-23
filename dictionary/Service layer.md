---
description: An application boundary that exposes use cases and coordinates transactions, domain objects and infrastructure.
---

A service layer is the set of application operations that sits between callers, such as controllers, CLI commands and queue consumers, and the business logic underneath. Each operation represents one use case, such as `placeOrder` or `cancelSubscription`, and coordinates loading data, calling domain objects, committing a transaction and triggering side effects. Martin Fowler's Patterns of Enterprise Application Architecture (2002) catalogues the pattern.

```typescript
class OrderService {
  constructor(private uow: UnitOfWork, private mailer: Mailer) {}

  async cancel(orderId: OrderId, actor: UserId) {
    const order = await this.uow.orders.get(orderId);
    const refund = order.cancel(actor);
    await this.uow.refunds.add(refund);
    await this.uow.commit();
    await this.mailer.sendCancellation(order);
  }
}
```

The pattern addresses one operation being implemented several times. When checkout logic lives in an HTTP controller, the nightly job and the admin CLI either call the endpoint over HTTP or copy the code, and the copies drift. With a service layer, all three call the same method, and the controller only parses the request and formats the response. The operation is also a natural place to hold a [unit of work](./Unit%20of%20work.md).

A service layer should coordinate rather than decide. When it accumulates conditionals about order state, the domain objects become data holders and the design has moved towards an [anemic domain model](./Anemic%20domain%20model.md). A single `OrderService` of several thousand lines is a common sign, and is a form of [god object](./God%20object.md). Split services by use case and push rules down onto the objects that own the data.

The pattern is often confused with two similar ones:

| Concept                                | Responsibility                       | Example                |
| -------------------------------------- | ------------------------------------ | ---------------------- |
| Service layer                          | Orchestrates a use case              | `OrderService.cancel`  |
| [Domain service](./Domain%20service.md) | Holds a rule spanning domain objects | `DiscountPolicy.quote` |
| [Facade](./Facade%20pattern.md)        | Simplifies a subsystem's interface   | `Payments.charge`      |

A small application with one delivery mechanism does not need this layer. A route handler written as a [transaction script](./Transaction%20script.md) is simpler until a second caller appears, and extracting a service at that point is a small refactor. Adding a service that only forwards each call to a repository creates indirection with no benefit.

_Usage:_

"The CLI refund skips the fraud check that the API runs."

"Each has its own copy. Move refunds into the service layer and have both call it."
