---
description: Bundling data with the operations on it and restricting outside access, so an object can protect its own rules.
---

Encapsulation is the bundling of data with the operations that act on it, along with restricting direct outside access to that data. In TypeScript this usually means a class with private fields and public methods, or a module that exports functions but not its internal state. The object controls how its data changes, so it can guarantee an [invariant](./Invariant.md).

The symptom of weak encapsulation is a value in an impossible state with no obvious culprit. An order has a negative total, or a `shipped` status with no shipping address, and finding the cause means searching every place that assigns to those fields, because any code can write to them.

```typescript
class Order {
  #items: LineItem[] = [];
  #status: "draft" | "placed" = "draft";

  addItem(item: LineItem) {
    if (this.#status !== "draft") throw new Error("Order is already placed");
    this.#items.push(item);
  }

  get items(): readonly LineItem[] {
    return this.#items;
  }
}
```

Private keywords alone do not achieve encapsulation. A private field with a public getter and setter offers the same access as a public field. Returning a mutable internal array lets callers change it from outside, which is why the getter above returns a `readonly` type. TypeScript's `private` is removed at compile time, while `#` fields are enforced at runtime.

Encapsulation is often conflated with [information hiding](./Information%20hiding.md). Encapsulation is a language mechanism for grouping and restricting access. Information hiding is a design decision about which details other modules should not depend on. A class can be fully encapsulated and still expose its design through a method such as `getMySqlConnection()`.

Not all data needs encapsulating. A [data transfer object](./Data%20transfer%20object.md) or a plain configuration record has no rules to protect, and wrapping it in accessors adds code without adding safety. Apply encapsulation where there are rules about how data may change. Domain objects that hold such rules outside themselves form an [anemic domain model](./Anemic%20domain%20model.md).

_Usage:_

"How did this order get shipped with no address?"

"Four services set `status` directly. Make it private and add a `ship()` method that checks the address."
