---
description: "Don't repeat yourself: each piece of knowledge should have one authoritative representation in a system."
---

DRY stands for "don't repeat yourself". Andy Hunt and Dave Thomas defined it in _The Pragmatic Programmer_ (1999): "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."

The principle concerns knowledge rather than text. A tax rate, a validation rule or the definition of an active customer should live in one place. When it is duplicated, the symptom is a fix applied in three places out of four: the checkout shows one price, the invoice shows another, and nobody knows which is correct. The scattered edits that follow are known as [shotgun surgery](./Shotgun%20surgery.md).

Code that looks the same is not always the same knowledge. Two functions may both check that a string is under 100 characters, one for a username and one for a product title. They match by coincidence and will change for different reasons. Merging them creates [coupling](./Coupling.md) between unrelated features, and the shared helper gradually gains flags such as `isAdmin` or `skipValidation` as each caller's needs diverge.

| Duplication    | Example                                 | Action                |
| -------------- | --------------------------------------- | --------------------- |
| Same knowledge | Tax rate defined in two services        | Consolidate           |
| Coincidental   | Similar validation for unrelated fields | Leave it              |
| Unclear        | Two similar handlers                    | Wait for a third case |

The last row reflects a common rule of thumb called the rule of three: tolerate a second copy and extract on the third, when the shared shape is visible. Extracting sooner risks a [premature abstraction](./Premature%20abstraction.md). Undoing a wrong abstraction usually costs more than removing duplication, because every caller has to be untangled.

DRY has a further cost across service or team boundaries. A shared library used by several services means a change can require coordinated releases, which can produce a [distributed monolith](./Distributed%20monolith.md). Duplicating a small amount of code between independently deployed services is often the better trade-off.

_Usage:_

"These two handlers have the same ten lines. Should I extract a helper?"

"One's for refunds, one's for payouts, and finance keeps changing them separately. Leave them apart for now."
