---
description: Adding new operations to a set of classes by placing them in separate visitor objects instead of editing each class.
---

The visitor pattern moves an operation out of a group of classes and into a separate visitor object that has one method per class. It is a behavioural pattern from the Gang of Four book (1994). Each element implements `accept(visitor)` and calls the visitor method for its own type. This technique, called double dispatch, selects the code to run from both the element's type and the visitor's type.

```typescript
interface ShapeVisitor<R> {
  visitCircle(shape: Circle): R;
  visitSquare(shape: Square): R;
}

class Circle {
  constructor(readonly radius: number) {}
  accept<R>(visitor: ShapeVisitor<R>) {
    return visitor.visitCircle(this);
  }
}

class Square {
  constructor(readonly side: number) {}
  accept<R>(visitor: ShapeVisitor<R>) {
    return visitor.visitSquare(this);
  }
}

const area: ShapeVisitor<number> = {
  visitCircle: (c) => Math.PI * c.radius ** 2,
  visitSquare: (s) => s.side ** 2,
};
```

The pattern addresses operations that keep landing on stable classes. In a compiler, the syntax node types change rarely, but type checking, linting, formatting and code generation all need to handle each node. Placing all of that on the nodes bloats them. The alternative is `instanceof` chains across the codebase, where a new node type is silently ignored by any chain that was not updated. With a visitor, adding a method to the interface produces a compile error in every visitor that lacks it. ESLint rules and Babel plugins use a visitor-style API keyed by node type.

The design makes one kind of change easy at the expense of another:

| Change              | With visitor       | With methods on each class |
| ------------------- | ------------------ | -------------------------- |
| Add an operation    | One new visitor    | Edit every class           |
| Add an element type | Edit every visitor | One new class              |

Use it only when the element types are stable. Visitors also often need access to element internals, which can weaken [encapsulation](./Encapsulation.md).

In TypeScript, a discriminated union and an exhaustive `switch` usually give the same benefits with less ceremony, since there is no `accept` and the compiler still reports unhandled cases:

```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "square"; side: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side ** 2;
  }
}
```

A visitor differs from an [iterator](./Iterator%20pattern.md): an iterator provides the next element, while a visitor defines what to do with each type of element. It is often applied across a [composite](./Composite%20pattern.md) tree.

_Usage:_

"We added a new AST node and the formatter silently dropped it."

"The formatter uses `instanceof` checks. Make it a visitor so a new node type is a compile error."
