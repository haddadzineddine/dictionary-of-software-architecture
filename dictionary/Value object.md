---
description: An immutable domain object defined entirely by its attributes, with no identity of its own.
---

A value object is a domain object defined entirely by its attributes, with no identity of its own. Two `Money` objects of 10 euros are interchangeable, in the way that two ten-euro notes are for most purposes. Common examples are money, date ranges, addresses, coordinates and email addresses. Eric Evans described the pattern in Domain-Driven Design (2003).

```typescript
class Money {
  private constructor(readonly cents: number, readonly currency: string) {}

  static of(cents: number, currency: string) {
    if (!Number.isInteger(cents)) throw new Error("Cents must be an integer");
    return new Money(cents, currency);
  }

  add(other: Money) {
    if (other.currency !== this.currency) throw new Error("Currency mismatch");
    return new Money(this.cents + other.cents, this.currency);
  }

  equals(other: Money) {
    return this.cents === other.cents && this.currency === other.currency;
  }
}
```

Value objects address rules scattered around primitive fields. When money is a `number`, nothing stops code from adding euros to dollars, and floating-point arithmetic can leave an invoice one cent out. This is [primitive obsession](./Primitive%20obsession.md). A `Money` type puts the currency check and integer arithmetic in one place, and any instance that exists is valid because its constructor enforced the [invariants](./Invariant.md).

Value objects are immutable, so an operation returns a new instance and leaves the original unchanged. This removes a class of aliasing bugs, such as two orders sharing one mutable `Address`, where editing one changes the other's delivery address.

| Property   | Value object         | [Entity](./Entity.md)      |
| ---------- | -------------------- | -------------------------- |
| Defined by | Attributes           | Identity                   |
| Equality   | All attributes match | Same ID                    |
| Mutability | Immutable            | Changes over its lifecycle |
| Lifecycle  | Created and replaced | Tracked over time          |
| Example    | `Money`, `DateRange` | `Customer`, `Order`        |

The same concept can be either, depending on the domain. An address is a value object for an online shop, where only its contents matter, and may be an entity for a postal service that tracks each delivery point over time.

Value objects are usually stored as columns on the owning table or as a JSON field, without an ID of their own. They are unnecessary for a field with no rules, so introduce them where a value has validation, units or operations. A value object differs from a [data transfer object](./Data%20transfer%20object.md), which only carries data across a boundary and enforces nothing.

_Usage:_

"The invoice total is off by a cent, and one line is in dollars."

"Prices are plain numbers. Introduce a `Money` value object that stores cents and rejects mixed currencies."
