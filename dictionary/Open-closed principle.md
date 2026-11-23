---
description: Software should be open to extension but closed to modification, so new behaviour does not require editing working code.
---

The open-closed principle says a module should be open for extension and closed for modification, so that new behaviour can be added without editing code that already works. Bertrand Meyer stated it in _Object-Oriented Software Construction_ (1988), using inheritance. Robert C. Martin later reframed it around interfaces and polymorphism, and it became the O in [SOLID](./SOLID.md).

The symptom is a `switch` that every new feature has to edit. Adding a payment method means changing the checkout function, the refund function and the receipt function, and each edit risks breaking the methods that already work.

```typescript
interface PaymentMethod {
  charge(amount: Money): Promise<Receipt>;
  refund(receipt: Receipt): Promise<void>;
}

// A new provider is a new class. checkout() does not change.
async function checkout(method: PaymentMethod, amount: Money) {
  return method.charge(amount);
}
```

The variation now sits behind an interface, usually through the [strategy pattern](./Strategy%20pattern.md) or a [plugin architecture](./Plugin%20architecture.md). The calling code stays closed, and each new variant is a new module.

No design is closed against every kind of change. The interface above makes adding a payment method cheap, but adding an operation such as `authorize` requires editing every implementation. A `switch` has the reverse trade-off: a new operation is one new function, while a new variant touches all of them. Choose based on which of the two actually changes in your system.

Avoid building extension points in advance. Guessing at future variation produces [speculative generality](./Speculative%20generality.md), and the guess is often wrong. Write the direct version first, then introduce an [abstraction](./Abstraction.md) when a second or third variant shows what really differs. For a closed set of cases that rarely changes, such as days of the week, a `switch` with exhaustive type checking is simpler.

_Usage:_

"Every new payment provider means editing five `switch` statements."

"We have four providers and more coming. Let's move them behind a `PaymentMethod` interface."
