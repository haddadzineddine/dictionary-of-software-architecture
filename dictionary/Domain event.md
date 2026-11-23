---
description: An immutable record of something meaningful that happened in a business domain, named in the past tense.
---

A domain event is an immutable record of something meaningful that happened in a business domain, named in the past tense. Examples are `OrderPlaced`, `PaymentFailed` and `SubscriptionCancelled`. An [aggregate](./Aggregate.md) typically records the event when its state changes, and other parts of the system react to it.

```typescript
type OrderPlaced = {
  type: "OrderPlaced";
  orderId: OrderId;
  customerId: CustomerId;
  total: Money;
  occurredAt: Date;
};
```

Domain events address workflows where one function must know every consequence of an action. A `placeOrder` function starts by saving the order, then gains calls to reserve stock, send an email, update analytics and award loyalty points. Each new requirement edits the same function, and an analytics timeout can fail the checkout. With an event, `placeOrder` records `OrderPlaced` and each reaction subscribes separately, similar to the [observer pattern](./Observer%20pattern.md) at the level of the business.

| Message           | Form                  | Meaning                            | Recipients     |
| ----------------- | --------------------- | ---------------------------------- | -------------- |
| Command           | Imperative, `PlaceOrder` | A request that can be rejected  | One handler    |
| Domain event      | Past, `OrderPlaced`   | A fact that has already happened   | Zero or more   |
| Integration event | Past, versioned       | A fact published to other contexts | Other services |

Domain events are usually internal to a bounded context, so their shape can change with the model. Publishing them unchanged to other teams turns internal structure into a public contract. Translate them to a stable integration event at the boundary.

Delivery introduces failure modes. If code commits the order and crashes before publishing, the event is lost and the stock is never reserved. The outbox pattern addresses this by writing the event in the same transaction as the state change. Handlers must also tolerate duplicates and out-of-order delivery when messages cross a broker.

Events make control flow harder to follow, because a reader of `placeOrder` cannot see what happens next. Reserve them for facts other parts of the system care about, since a simple two-step operation is clearer as a direct call. Domain events are also distinct from event sourcing, which stores events as the system of record. A system can use domain events with ordinary state tables.

_Usage:_

"An analytics timeout failed the checkout again."

"Checkout shouldn't know about analytics. Publish `OrderPlaced` and let analytics consume it separately."
