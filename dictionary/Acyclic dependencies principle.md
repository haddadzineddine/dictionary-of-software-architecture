---
description: The dependency graph between packages must contain no cycles, so each package can be built, tested and released separately.
---

The acyclic dependencies principle says the dependency graph between packages must have no cycles. Robert C. Martin defined it among his package design principles. Following dependencies from any package should never lead back to where you started, which makes the graph a directed acyclic graph.

It addresses what Martin called the "morning after syndrome". A developer's code worked yesterday, but today it fails because someone changed a package it depends on. Teams respond by coordinating releases, and when packages depend on one another in a loop, none can be released without the others. A [circular dependency](./Circular%20dependency.md) turns those packages into one large unit for building, testing and versioning, even though they live in separate directories.

| Graph   | Build order                      | Effect of a change                 |
| ------- | -------------------------------- | ---------------------------------- |
| Acyclic | A clear order from the leaves up | Affects only dependents            |
| Cyclic  | No valid order                   | Affects every package in the cycle |

```text
Before:  billing -> orders -> customers -> billing

After:   billing -> orders -> customers -> billing-api
         billing -> billing-api
```

Two standard techniques break a cycle. The first is the [dependency inversion principle](./Dependency%20inversion%20principle.md): one package depends on an interface, and the other implements it, as `billing` implements `billing-api` above. The second is to extract the code both packages use into a new package that they both depend on. If the packages are really one concept, merging them is also an option.

Cycles are easier to prevent than to remove. They usually arrive through one small convenience import during ordinary work, so enforce the rule with a dependency check in CI, which acts as a [fitness function](./Fitness%20function.md). Once several cycles have formed, separating them takes planned effort, and the codebase drifts toward a [big ball of mud](./Big%20ball%20of%20mud.md).

The principle pairs with the [stable dependencies principle](./Stable%20dependencies%20principle.md), which governs the direction the arrows should point. Cycles inside a single package are a smaller concern because the package is released as a unit, though they can still cause load-order errors.

_Usage:_

"Why can't we release `orders` without also releasing `billing`?"

"They depend on each other through `customers`. Extract a `billing-api` package to break the cycle."
