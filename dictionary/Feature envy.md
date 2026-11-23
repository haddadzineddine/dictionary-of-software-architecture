---
description: A code smell where a method uses another object's data more than its own, suggesting it belongs elsewhere.
---

Feature envy is a code smell in which a method uses another object's data more than its own, which suggests the method belongs on that other object. Martin Fowler and Kent Beck described it in _Refactoring_ (1999). It is recognisable when every line of a method starts with `customer.`, and when renaming a field on `Customer` forces edits in `InvoiceService`.

```typescript
// Envious: the rule reads only Customer data.
class InvoiceService {
  discountRate(customer: Customer): number {
    if (customer.isSuspended) return 0;
    if (customer.loyaltyYears >= 5) return 0.1;
    return customer.orderCount > 20 ? 0.05 : 0;
  }
}

// Moved: the rule sits with the data it reads.
class Customer {
  discountRate(): number {
    if (this.isSuspended) return 0;
    if (this.loyaltyYears >= 5) return 0.1;
    return this.orderCount > 20 ? 0.05 : 0;
  }
}
```

The envious version forces `Customer` to expose its fields, which weakens [encapsulation](./Encapsulation.md) and adds [coupling](./Coupling.md) between the two classes. A change to loyalty rules also lands in a class about invoices. [Tell don't ask](./Tell%20don't%20ask.md) gives the matching guidance: ask an object to do the work instead of pulling its data out. Long chains such as `order.customer.address.city` often accompany this smell and break the [Law of Demeter](./Law%20of%20Demeter.md). When envy is repeated across a codebase, the result is an [anemic domain model](./Anemic%20domain%20model.md).

To fix it, move the method to the class whose data it uses. If only part of the method is envious, extract that part and move it. If a method uses data from two objects, place it with the data that changes alongside the rule.

Some designs separate behaviour from data on purpose. A [visitor](./Visitor%20pattern.md) reads other objects' data so that operations can vary independently of them. A report formatter also reads many `Customer` fields, but moving it onto `Customer` would pull presentation into the domain and work against [separation of concerns](./Separation%20of%20concerns.md). Ask what causes the code to change. If it changes with customer rules, move it. If it changes with the report layout, leave it.

_Usage:_

"`discountRate` is in `InvoiceService`, but it only reads `Customer` fields."

"And it changes whenever the loyalty rules change. Move it onto `Customer`."
