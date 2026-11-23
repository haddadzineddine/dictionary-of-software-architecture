---
description: A guideline that a method should call only its close collaborators, not reach through them into objects further away.
---

The Law of Demeter is a guideline that a method should only talk to its immediate collaborators. It came from the Demeter project at Northeastern University in the late 1980s and is often summarised as "only talk to your friends". A method may call methods on itself, its parameters, objects it creates and its own fields.

The symptom is a chain of property accesses that reaches through several objects, often called a train wreck:

```typescript
// Reaches through customer, wallet and card
order.customer.wallet.primaryCard.charge(total);

// Tells the order what should happen
order.chargeCustomer(total);
```

The first line depends on the shape of four objects. When `wallet` becomes optional or customers get several payment methods, every caller with that chain breaks, and the fix spreads across the codebase as [shotgun surgery](./Shotgun%20surgery.md). Tests also suffer, because a mock has to return a mock that returns a mock.

Each reach adds [coupling](./Coupling.md) to a structure the caller should not need to know about. Following the law moves behaviour to the object that owns the data, which is the same direction as [tell don't ask](./Tell%20don't%20ask.md).

The law is not about counting dots:

| Code                                | Violation? | Why                                   |
| ----------------------------------- | ---------- | ------------------------------------- |
| `order.customer.wallet.primaryCard` | Yes        | Navigates another object's internals  |
| `items.filter(isPaid).map(toTotal)` | No         | Each call returns a new collection    |
| `query.where(a).orderBy(b)`         | No         | A fluent builder returns itself       |
| `dto.address.city`                  | Usually no | Plain data with no behaviour to hide  |

Applied rigidly, the law produces wrapper methods such as `order.getCustomerWalletCardLast4()` that only forward calls, and the outer class grows with every new need. If many such forwards accumulate, the data may be in the wrong place, or the caller may need a different object passed in directly. Passing `card` as a parameter is often simpler than adding a method to reach it.

_Usage:_

"Making `wallet` optional broke forty call sites."

"They all reach through `customer.wallet.primaryCard`. Put a method on `Customer` so the path lives in one place."
