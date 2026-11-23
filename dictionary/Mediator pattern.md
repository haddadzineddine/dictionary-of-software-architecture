---
description: Routing communication between objects through one coordinator so they do not refer to each other directly.
---

The mediator pattern places a coordinator between a group of objects, called colleagues, so that they communicate through it instead of referring to each other directly. It is a behavioural pattern from the Gang of Four book (1994). Each colleague knows only the mediator, and the mediator holds the rules for how they interact.

```typescript
interface CheckoutMediator {
  notify(event: "countryChanged" | "couponApplied"): void;
}

class CheckoutForm implements CheckoutMediator {
  constructor(
    private shipping: ShippingPicker,
    private tax: TaxSummary,
    private total: OrderTotal,
  ) {}

  notify(event: "countryChanged" | "couponApplied") {
    if (event === "countryChanged") this.shipping.reload();
    this.tax.recalculate();
    this.total.refresh();
  }
}
```

The pattern addresses a web of direct references. In a form where the country field updates shipping, shipping updates tax, tax updates the total and the coupon field touches all three, each component imports its neighbours. Changing one breaks others, none can be reused alone, and a [circular dependency](./Circular%20dependency.md) can appear. Connecting n objects to one another requires up to n(n-1)/2 links. With a mediator, it takes n.

Interaction logic then lives in a single class, which is easier to read and change, and each colleague has lower [coupling](./Coupling.md). A parent component that holds shared state and passes callbacks to its children is a familiar example in UI frameworks.

The risk is that the mediator absorbs everything. As rules accumulate, it can turn into a [god object](./God%20object.md) that every feature must edit. Keep it limited to coordination, leave business rules in the colleagues or domain objects, and split it when it serves unrelated workflows.

The mediator is often compared with two other patterns:

| Pattern                             | Who knows whom                                  | Direction              |
| ----------------------------------- | ----------------------------------------------- | ---------------------- |
| Mediator                            | Colleagues know the mediator, which knows them  | Two-way coordination   |
| [Observer](./Observer%20pattern.md) | Subject does not know what its observers do     | One-way notification   |
| [Facade](./Facade%20pattern.md)     | Callers know the facade; the subsystem does not | One-way simplification |

A mediator is often implemented with observers: colleagues emit events and the mediator listens. The distinction is that a mediator holds the coordination logic, while plain observers react independently.

Do not add a mediator for two objects that interact in one simple way. A direct call is easier to follow.

_Usage:_

"Changing the country picker broke the coupon field again."

"They all call each other. Have the form mediate, so each field only reports that it changed."
