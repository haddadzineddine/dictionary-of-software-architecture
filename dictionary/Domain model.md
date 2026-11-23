---
description: An object model of a business in which data and behaviour live together and the objects enforce the rules.
---

A domain model is a set of objects that represent the concepts of a business, with each object holding both its data and the rules that apply to that data. An `Order` knows whether it can be cancelled, and calling code asks it to cancel instead of editing a status field. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002), and Eric Evans built a modelling practice around it in Domain-Driven Design (2003).

```typescript
class Order {
  private status: "open" | "shipped" | "cancelled" = "open";

  constructor(private readonly lines: OrderLine[]) {}

  cancel(): Refund {
    if (this.status === "shipped") throw new OrderAlreadyShipped();
    this.status = "cancelled";
    return Refund.forLines(this.lines);
  }
}
```

The pattern addresses business rules scattered across handlers. When the cancellation check lives in four [transaction scripts](./Transaction%20script.md), a rule change needs four edits, and the missed one appears as a refund on a shipped order. In a domain model, the rule has one location, and [encapsulation](./Encapsulation.md) stops other code from bypassing it. Conditions that must always hold, known as [invariants](./Invariant.md), can be checked by the object that owns the state.

A domain model has costs. Objects shaped around business concepts rarely match database tables, so persistence usually needs a [data mapper](./Data%20mapper.md). The team also has to learn the business well enough to model it, and early models are often wrong and need reshaping. For an application that mostly stores and displays records, this structure adds ceremony without protecting any rule, and transaction scripts or [active record](./Active%20record.md) are simpler.

The term is also used loosely for any diagram or set of classes describing a business. In the pattern sense, data classes with public setters and all logic held in services do not qualify. That arrangement is an [anemic domain model](./Anemic%20domain%20model.md), which carries the cost of the extra classes without keeping rules beside the data.

A practical approach is to apply a domain model only to the parts of a system where rules are complicated or change often, and leave the rest simple. Names in the model should match the [ubiquitous language](./Ubiquitous%20language.md) that domain experts use.

_Usage:_

"Where does the rule for cancelling an order live?"

"In four handlers. Move it onto `Order` so there is one version to change."
