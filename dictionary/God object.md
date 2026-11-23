---
description: A class that holds too much data and too many responsibilities, so unrelated features all depend on it and change it.
---

A god object is a class that holds too much data and too many responsibilities, so most of the system depends on it. It often has a broad name such as `UserManager`, `AppService` or `OrderManager`. The symptoms are practical: every pull request conflicts in the same file, a unit test needs a dozen mocks before it can run, and nobody can state the purpose of the class in one sentence.

```typescript
class OrderManager {
  createOrder(input: OrderInput) {}
  applyDiscount(orderId: string, code: string) {}
  chargeCard(orderId: string) {}
  sendConfirmationEmail(orderId: string) {}
  generateInvoicePdf(orderId: string) {}
  syncToWarehouse(orderId: string) {}
  exportMonthlyReport(month: string) {}
}
```

This class breaks the [single responsibility principle](./Single%20responsibility%20principle.md), because payment, tax, email and reporting changes all land in it. Its [cohesion](./Cohesion.md) is low, since most methods share little state. Its [coupling](./Coupling.md) is high, since many callers depend on it and it depends on many services. A change for one feature can therefore break another.

God objects grow because they are convenient. The class already has access to everything, so adding one more method is quicker than designing a new module. Each addition makes the next one more likely.

To break one up, group its methods by the data they use and the reason they change. Extract one group at a time into a class such as `Invoicing` or `Payments`. During the migration, the original class can act as a [facade](./Facade%20pattern.md) that delegates to the new classes, so callers can move gradually. Remove the delegating methods once nothing calls them.

Size alone does not make a class a god object. A [deep module](./Deep%20module.md) can hide a large implementation behind a small interface, and a long parser may do only one thing. A facade also has a broad reach, but it coordinates other objects and holds little logic of its own. The test is whether the responsibilities are related and change for the same reasons.

_Usage:_

"Three of us have merge conflicts in `OrderManager` again."

"It handles payments, invoices and emails. Let's extract invoicing first and have the old method delegate to it."
