---
description: High-level policy and low-level details should both depend on abstractions, so business rules do not import infrastructure.
---

The dependency inversion principle says high-level modules should not depend on low-level modules, and that both should depend on [abstractions](./Abstraction.md). It is the D in [SOLID](./SOLID.md), stated by Robert C. Martin. In practice, business rules define the interface they need, and infrastructure implements it.

The symptom is business logic that cannot run without its infrastructure. Testing a pricing rule requires a running database, or replacing an email vendor means editing the order code, because `OrderService` imports the vendor SDK directly.

```typescript
// orders/order-service.ts: the policy owns the interface
export interface Notifier {
  orderPlaced(order: Order): Promise<void>;
}

export class OrderService {
  constructor(private notifier: Notifier) {}

  async place(order: Order) {
    await this.notifier.orderPlaced(order);
  }
}

// infrastructure/email-notifier.ts: the detail depends on the policy
import type { Notifier } from "../orders/order-service";

export class EmailNotifier implements Notifier {
  async orderPlaced(order: Order) {
    /* call the vendor API */
  }
}
```

The inversion refers to the direction of the source-code dependency. Control still flows from `OrderService` to the email code at runtime, but the import arrow now points from infrastructure toward the business rules. The location of the interface matters: if it sits in the infrastructure package, the business code still depends on that package and nothing has been inverted.

Three related terms are often confused:

| Term                                                | What it is                                               |
| --------------------------------------------------- | -------------------------------------------------------- |
| Dependency inversion                                | A design rule about which way source dependencies point  |
| Dependency injection                                | A technique for passing a dependency in from outside     |
| [Inversion of control](./Inversion%20of%20control.md) | A framework or caller decides when your code runs      |

This rule underpins [clean architecture](./Clean%20architecture.md), [onion architecture](./Onion%20architecture.md) and hexagonal architecture. It costs an interface and a wiring step at each boundary. Apply it where the detail is likely to change or is awkward to test, such as databases, payment gateways and third-party APIs. Wrapping a stable utility library or a pure function adds indirection with no benefit.

_Usage:_

"We can't test the discount logic without Postgres running."

"It imports the client directly. Have the service define a small interface and pass the Postgres version in at startup."
