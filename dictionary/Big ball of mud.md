---
description: A system with no recognisable structure, where any part can depend on any other and changes have unpredictable effects.
---

A big ball of mud is a system with no recognisable structure, in which any part can depend on any other. Brian Foote and Joseph Yoder named it in their 1997 paper "Big Ball of Mud" and treated it as a common outcome in working software, not a rare failure. The usual symptom is a change with a distant effect: a fix to invoice rounding breaks the password reset email, and nobody can explain why until they trace a chain of shared helpers.

The structure erodes through many decisions that were reasonable at the time. Deadlines, staff turnover and changing requirements each encourage a shortcut, and each shortcut adds a dependency. With no enforced boundaries, [coupling](./Coupling.md) rises and [circular dependencies](./Circular%20dependency.md) appear. This is [architectural drift](./Architectural%20drift.md) left unchecked. New engineers need months before they can change anything alone, and tests require most of the application to start.

A big ball of mud is different from a monolith. A monolith with clear internal modules is well structured inside one deployable. A set of microservices can have no structure at all, which produces a [distributed monolith](./Distributed%20monolith.md).

A full rewrite is rarely the right response, because many business rules exist only in the code and are easy to lose. Incremental work is safer:

| Step | Action                                                                     |
| ---- | -------------------------------------------------------------------------- |
| 1    | Map the actual dependencies with a tool                                    |
| 2    | Choose one area that changes often                                         |
| 3    | Add characterisation tests that record its current behaviour               |
| 4    | Introduce a [seam](./Seam.md) and move callers behind an interface         |
| 5    | Enforce the new boundary in CI with a [fitness function](./Fitness%20function.md) |

Repeat this for the areas that change most. Untidy code that is stable and rarely touched can stay as it is. A throwaway prototype can also be built without structure at little cost, provided it is actually thrown away.

_Usage:_

"Why did changing invoice rounding break the password reset email?"

"Both import the same utils module, and that module imports half the app. Let's map the dependencies before we change anything else."
