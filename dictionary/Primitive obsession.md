---
description: Using strings, numbers and booleans for domain concepts that should have their own types and validation.
---

Primitive obsession is the use of strings, numbers and booleans to represent domain concepts that should have their own types. Martin Fowler and Kent Beck listed it as a code smell in _Refactoring_ (1999). Common examples are money stored as a `number`, email addresses as a `string` and identifiers as plain strings. The symptoms are concrete: a caller swaps `userId` and `orderId` and the compiler accepts it, an amount in cents is added to an amount in euros, and the same email regex appears in four files with small differences.

```typescript
// Compiles, even with the arguments in the wrong order.
function transfer(from: string, to: string, amount: number) {}
transfer(customerId, accountId, priceInCents);

// A branded type stops one kind of ID being passed as another.
type AccountId = string & { readonly __brand: "AccountId" };

// A value object validates once and carries its operations.
class Money {
  private constructor(readonly cents: number, readonly currency: "EUR" | "USD") {}

  static of(cents: number, currency: "EUR" | "USD") {
    if (!Number.isInteger(cents)) throw new Error("Cents must be an integer");
    return new Money(cents, currency);
  }

  add(other: Money) {
    if (other.currency !== this.currency) throw new Error("Currency mismatch");
    return new Money(this.cents + other.cents, this.currency);
  }
}
```

The usual fix is a [value object](./Value%20object.md). It wraps the primitive, validates at construction so that its [invariant](./Invariant.md) holds wherever the value travels, and provides the operations that make sense for it. `Money` can refuse to add two currencies, which a `number` cannot do. For identifiers that need no behaviour, a branded type in TypeScript gives compile-time safety at no runtime cost.

Wrapping has a cost. Values must be converted at boundaries such as database rows, JSON and form input. Parse them once at the boundary and pass the typed value from then on. A [data transfer object](./Data%20transfer%20object.md) may reasonably keep primitives because it exists for transport.

Not every string needs a class. A display label or a local loop counter gains nothing from wrapping. Introduce a type when a value has validation rules, a unit or format, or can be confused with another value of the same primitive type.

_Usage:_

"A refund went out at a hundred times the correct amount."

"One caller passed euros and the other expected cents. Let's replace that `number` with a `Money` type."
