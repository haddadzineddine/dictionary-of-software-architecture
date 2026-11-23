---
description: Defining interchangeable algorithms behind one interface so the one in use can be selected at runtime.
---

The strategy pattern defines a family of interchangeable algorithms behind one interface, so the code that uses them can switch between them without changing. It is a behavioural pattern from the Gang of Four book (1994). The object that uses an algorithm, called the context, holds a reference to a strategy and delegates that part of its work.

```typescript
type PricingStrategy = (subtotal: number) => number;

const standard: PricingStrategy = (subtotal) => subtotal;
const member: PricingStrategy = (subtotal) => subtotal * 0.9;
const bulk: PricingStrategy = (subtotal) => (subtotal > 1000 ? subtotal * 0.8 : subtotal);

function checkout(cart: Cart, pricing: PricingStrategy) {
  return pricing(cart.subtotal) + cart.shipping;
}
```

In languages with first-class functions, a strategy is often a plain function, as above, and needs no class hierarchy. Use a class or object when the strategy needs configuration, holds state or has several related methods.

The pattern addresses branching that keeps growing. A `calculatePrice` function with an `if` for each customer tier gets longer with every promotion, each edit risks breaking existing tiers, and the tests must cover all paths through one function. Separate strategies can be added without changing the context, in line with the [open-closed principle](./Open-closed%20principle.md), and each can be tested alone.

Selection still has to happen somewhere. Put the mapping from configuration to strategy in one place, such as a lookup table or [factory method](./Factory%20method.md), so the conditional is not copied to every call site. All strategies must also honour the same contract. If one returns cents while another returns dollars, the type checker accepts both and the caller gets wrong totals, a violation of the [Liskov substitution principle](./Liskov%20substitution%20principle.md).

The strategy is commonly confused with two patterns:

| Pattern                                   | What varies                    | How                               |
| ----------------------------------------- | ------------------------------ | --------------------------------- |
| Strategy                                  | A complete algorithm           | Composition, chosen by the caller |
| [State](./State%20pattern.md)             | Behaviour across a lifecycle   | The object transitions itself     |
| [Template method](./Template%20method.md) | Steps within a fixed algorithm | Inheritance                       |

Do not introduce strategies when there are two branches that rarely change. A single `if` is easier to read than an interface, several implementations and a selection mechanism, and extracting it early is [premature abstraction](./Premature%20abstraction.md).

_Usage:_

"Every new promotion means another branch in `calculatePrice`, and last week's broke member pricing."

"Make each pricing rule a strategy and select it from a lookup table."
