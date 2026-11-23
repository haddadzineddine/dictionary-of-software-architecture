---
description: Any subtype must be usable wherever its parent type is expected, without surprising the code that relies on it.
---

The Liskov substitution principle says that code written against a type must keep working when given any of its subtypes. Barbara Liskov introduced the idea in a 1987 keynote, and she and Jeannette Wing formalised it in a 1994 paper. It is the L in [SOLID](./SOLID.md).

The compiler checks method signatures but not behaviour, so a subtype can type-check and still break its callers. The symptom is an `instanceof` check added to a caller because one subclass behaves differently, or a method that throws `NotImplementedError` in one subclass.

```typescript
class Rectangle {
  constructor(public width: number, public height: number) {}
  setWidth(w: number) { this.width = w; }
  area() { return this.width * this.height; }
}

class Square extends Rectangle {
  setWidth(w: number) { this.width = w; this.height = w; }
}

// With a height of 4, a Rectangle returns 20. A Square returns 25.
function stretch(r: Rectangle) {
  r.setWidth(5);
  return r.area();
}
```

A subtype must honour the contract of its parent:

| Rule                         | Meaning                           | Violation                                  |
| ---------------------------- | --------------------------------- | ------------------------------------------ |
| Preconditions                | Cannot demand more from callers   | Rejects input the parent accepts           |
| Postconditions               | Cannot promise less               | Returns `null` where the parent never does |
| [Invariants](./Invariant.md) | Must preserve what is always true | `Square` ties width to height              |
| Exceptions                   | Cannot add new kinds of failure   | `ReadOnlyList.add()` throws                |

The fix is usually to remove the inheritance relationship. "Is a" in everyday language does not imply substitutability: a square is a rectangle in geometry, but it is not a mutable `Rectangle` object. Use a narrower shared interface such as `Shape { area(): number }`, or apply [composition over inheritance](./Composition%20over%20inheritance.md).

The principle applies beyond classes. A new version of an API, a replacement storage driver and a fake used in tests are all substitutes, and each must honour what callers rely on.

_Usage:_

"Why is there an `instanceof ReadOnlyCache` check in the save path?"

"Its `set` throws, so it can't stand in for `Cache`. Give it a read-only interface and stop inheriting."
