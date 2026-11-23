---
description: Organising code by feature or request, so each slice owns its logic and data access instead of sharing horizontal layers.
---

Vertical slice architecture organises code around individual features or requests rather than technical layers. Each slice contains what one operation needs: input validation, business logic, data access and response shape. Jimmy Bogard popularised the name.

It addresses changes that cut across every layer. Adding one field to an order screen in a layered codebase can mean editing a controller, a service, a repository, a [data transfer object](./Data%20transfer%20object.md) and a mapper in five folders. Shared services also accumulate methods for unrelated callers, so a change made for one feature breaks another.

```text
features/
  place-order/
    handler.ts
    validate.ts
    place-order.test.ts
  cancel-order/
    handler.ts
    cancel-order.test.ts
```

Slices favour high [cohesion](./Cohesion.md) within a feature and low [coupling](./Coupling.md) between features. Each slice can choose its own approach: a simple read may run one SQL query, while a complex write may use a rich [domain model](./Domain%20model.md).

The main risk is duplication. Two slices may implement the same business rule and then diverge, for example when refund eligibility is checked differently in two features. Move a rule to shared domain code once it is a genuine business concept, rather than at the first sign of similar code. Vertical slices also fit poorly when many features must enforce the same complex [invariants](./Invariant.md) over the same data, because those rules belong in a shared model.

Vertical slice architecture differs from [package by feature](./Package%20by%20feature.md), which is a rule for arranging folders. A package-by-feature codebase can still repeat the same layers inside every folder. Vertical slice architecture goes further by treating each request as an independent unit with its own implementation and minimal sharing.

_Usage:_

"Adding a coupon field touched eleven files across six folders."

"Move checkout into one slice. The next field should change one folder."
