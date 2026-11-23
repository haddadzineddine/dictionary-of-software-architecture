---
description: Representing a business rule as a combinable object that answers whether a candidate satisfies it.
---

The specification pattern represents a business rule as an object that answers whether a candidate satisfies it. Specifications can be combined with `and`, `or` and `not` to build larger rules from small named ones. Eric Evans and Martin Fowler described the pattern, and Evans includes it in Domain-Driven Design (2003).

```typescript
interface Specification<T> {
  isSatisfiedBy(candidate: T): boolean;
}

const and = <T>(a: Specification<T>, b: Specification<T>): Specification<T> => ({
  isSatisfiedBy: (c) => a.isSatisfiedBy(c) && b.isSatisfiedBy(c),
});

const isActive: Specification<Customer> = {
  isSatisfiedBy: (c) => c.status === "active",
};
const hasNoDebt: Specification<Customer> = {
  isSatisfiedBy: (c) => c.balance >= 0,
};
const canReorder = and(isActive, hasNoDebt);
```

The pattern addresses a rule written in several forms. The definition of a customer who can reorder may exist in a `WHERE` clause, a validation check and a UI condition. When the definition changes, one is missed, and the application offers a button that then fails at checkout. A specification gives the rule one name and one definition. Evans lists three uses: validating an object, selecting matching objects from a collection, and describing what something to be created must satisfy.

The main difficulty is the database. An `isSatisfiedBy` function runs in memory, so using it for selection means loading every row and filtering in the application, which passes in tests and times out on a production table. One solution is for each specification to also produce a query expression, which adds a small [interpreter](./Interpreter%20pattern.md) to the codebase and needs tests to keep the two forms consistent. Another is to build specifications on an ORM's query objects, which ties them to that ORM.

The pattern is unnecessary for most conditions. A named predicate such as `canReorder(customer)` provides one definition with far less machinery, and it is enough until rules must be combined at runtime or stored as configuration. Use the full pattern when the combinations themselves vary.

It differs from the [strategy pattern](./Strategy%20pattern.md). A strategy selects how to perform an operation, such as which pricing algorithm to run. A specification answers yes or no about a candidate. The two can work together, with a specification deciding which strategy applies.

_Usage:_

"The button says the customer can reorder, but checkout rejects them."

"The UI and checkout each have their own rule. Define `canReorder` once and have both call it."
