---
description: Moving state-specific behaviour into separate objects so an object changes how it acts when its state changes.
---

The state pattern moves behaviour that depends on an object's state into separate state objects. It is a behavioural pattern from the Gang of Four book (1994). The main object, called the context, delegates to its current state object, so it appears to change behaviour when the state changes.

```typescript
interface OrderState {
  pay(order: Order): void;
  ship(order: Order): void;
}

class Pending implements OrderState {
  pay(order: Order) {
    order.setState(new Paid());
  }
  ship() {
    throw new Error("Cannot ship an unpaid order");
  }
}

class Paid implements OrderState {
  pay() {
    throw new Error("Already paid");
  }
  ship(order: Order) {
    order.setState(new Shipped());
  }
}

class Shipped implements OrderState {
  pay() {
    throw new Error("Already paid");
  }
  ship() {
    throw new Error("Already shipped");
  }
}

class Order {
  private state: OrderState = new Pending();
  setState(state: OrderState) {
    this.state = state;
  }
  pay() {
    this.state.pay(this);
  }
  ship() {
    this.state.ship(this);
  }
}
```

The pattern addresses the same `switch (status)` repeated in every method. When a new status such as `refunded` is added, each switch must be updated, and a missed branch lets an order ship twice or be refunded before it was paid. With state objects, all behaviour for one status lives in one class, and the legal transitions are explicit. An illegal transition fails at the point it is attempted, which protects the object's [invariants](./Invariant.md).

In TypeScript, classes are often unnecessary. A discriminated union with a `transition(state, event)` function and an exhaustive `switch` produces compiler errors for missed cases and keeps state as plain data. This is usually the better choice when state is persisted, because class instances must be rebuilt from a database column anyway. For workflows with many states, guards and timers, a state machine library adds a formal model.

The state pattern is structurally almost identical to the [strategy pattern](./Strategy%20pattern.md). The difference is in who changes the object in use:

|                         | State                         | Strategy                   |
| ----------------------- | ----------------------------- | -------------------------- |
| Selected by             | The object's own transitions  | The caller, usually once   |
| Objects know each other | Often, to trigger transitions | No                         |
| Models                  | A lifecycle                   | Interchangeable algorithms |

Two or three statuses with a small amount of conditional logic do not need this pattern, because the indirection outweighs the benefit. Introduce it when the same status checks appear across many methods or when invalid transitions have caused bugs.

_Usage:_

"A cancelled order got shipped because `ship()` didn't check for the new status."

"Status checks are scattered across every method. Model the lifecycle as explicit states so illegal transitions fail."
