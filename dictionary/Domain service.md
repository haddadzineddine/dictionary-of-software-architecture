---
description: A stateless domain operation for a business rule that does not belong to a single entity or value object.
---

A domain service is a stateless operation that expresses a business rule which does not naturally belong to a single [entity](./Entity.md) or [value object](./Value%20object.md). Eric Evans described it in Domain-Driven Design (2003). It is named in business language and takes domain objects as arguments, such as `DiscountPolicy.priceFor(order, customer, promotions)`.

```typescript
class DiscountPolicy {
  priceFor(order: Order, customer: Customer, promotions: Promotion[]): Money {
    const best = promotions
      .filter((promotion) => promotion.appliesTo(order, customer))
      .map((promotion) => promotion.discountOn(order.total()))
      .reduce((a, b) => (a.greaterThan(b) ? a : b), Money.zero(order.currency));

    return order.total().subtract(best);
  }
}
```

The pattern addresses rules that make any host object awkward. A discount that depends on an order, a customer's tier and the active promotions could go on `Order`, but then `Order` must know about promotions and tiers. Signs of a misplaced method are a long parameter list of other objects, or a method that reads more from its arguments than from `this`, a smell known as [feature envy](./Feature%20envy.md). Moving the rule to a domain service keeps each object focused.

A domain service is easily confused with an application service in a [service layer](./Service%20layer.md):

| Aspect     | Domain service              | Application service                            |
| ---------- | --------------------------- | ---------------------------------------------- |
| Contains   | Business decisions          | Orchestration of a use case                    |
| Depends on | Domain objects              | Repositories, transactions, gateways           |
| Example    | Calculate the best discount | Load order, apply discount, commit, send email |
| Tested with | Plain objects              | Fakes or integration tests                     |

To tell them apart, ask whether a domain expert would recognise the operation and care about its rules. If so, it belongs in the domain. If it is about loading, saving or sending, it belongs in the application layer.

Overuse is the main risk. When teams place every rule in classes named `OrderManager` or `CustomerHelper`, the entities become data holders and the design turns into an [anemic domain model](./Anemic%20domain%20model.md). Put behaviour on an entity or value object first, and use a domain service only when that would make the model worse. Some domain services need outside data, such as an exchange rate. Define an interface in the domain and implement it in infrastructure, following the [dependency inversion principle](./Dependency%20inversion%20principle.md).

_Usage:_

"`Order` now imports `Promotion`, `CustomerTier` and `TaxTable`. Is that right?"

"No. Pricing spans all of them, so pull it into a `DiscountPolicy` domain service."
