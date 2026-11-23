---
description: The degree to which one module depends on another, judged by how likely a change in one forces a change in the other.
---

Coupling is the degree to which one module depends on another. Two modules are tightly coupled when a change in one is likely to require a change in the other, and loosely coupled when each can change independently. Larry Constantine developed the concept, and it was published with Edward Yourdon in _Structured Design_.

The symptom is a small change that spreads. Renaming a field breaks three services, one team's release waits on another team's, or a test fails in a module nobody touched.

The structured design scale lists these forms, from loosest to tightest:

| Form     | One module depends on                 | Example                         |
| -------- | ------------------------------------- | ------------------------------- |
| Data     | Only the values passed as parameters  | `tax(amount, rate)`             |
| Stamp    | A structure, using only part of it    | `tax(order)` reads one field    |
| Control  | A flag that steers the other's logic  | `render(data, isAdmin)`         |
| External | A shared format or protocol           | Two services parse the same file |
| Common   | Shared mutable global state           | A global `config` both modify   |
| Content  | Another module's internals            | Reading a private field         |

Coupling also exists outside the code. Temporal coupling means one service must be running for another to work. Deployment coupling means two components must be released together. A system split into services that must deploy together is a [distributed monolith](./Distributed%20monolith.md), which keeps the coupling of a monolith and adds network failure.

Some coupling is required, because modules that share nothing cannot cooperate. The goal is to make it deliberate: depend on a narrow, stable interface rather than on internals, and keep things that change together in the same module, which raises [cohesion](./Cohesion.md). Techniques include [information hiding](./Information%20hiding.md) and the [dependency inversion principle](./Dependency%20inversion%20principle.md). [Connascence](./Connascence.md) gives a finer vocabulary for describing how two pieces of code are linked.

Removing coupling can go too far. Replacing a direct function call with an event bus hides the dependency without removing it and makes the flow harder to trace.

_Usage:_

"Why does a change to the user table need a release from the billing team?"

"Billing reads that table directly. They're coupled to our schema, so give them an API instead."
