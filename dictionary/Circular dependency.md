---
description: Two or more modules that depend on each other directly or indirectly, so none can be loaded or understood alone.
---

A circular dependency exists when two or more modules depend on each other, directly or through a chain. For example, A imports B, B imports C, and C imports A. None of the modules in the cycle can be built, tested or understood alone.

In JavaScript and TypeScript, the symptom is often a runtime error that appears after an unrelated change: `Class extends value undefined is not a constructor`, `Cannot access 'X' before initialization`, or an imported value that is unexpectedly `undefined`. One module runs before the other has finished initialising, so reordering an import can make the bug appear or vanish.

```typescript
// user.ts
import { sendWelcome } from "./email";
export const DEFAULT_SENDER = "hello@example.com";
export const signUp = (to: string) => sendWelcome(to);

// email.ts
import { DEFAULT_SENDER } from "./user";
const sender = DEFAULT_SENDER.toLowerCase(); // Throws when user.ts loads first
export const sendWelcome = (to: string) => deliver(sender, to);
```

`import type` statements are erased at compile time, so type-only cycles do not fail at runtime, although they can still show a design problem.

Beyond load errors, a cycle is [coupling](./Coupling.md) that prevents independent change. Modules in a cycle effectively form one module and must be released together. The [acyclic dependencies principle](./Acyclic%20dependencies%20principle.md) states this rule at the package level.

| Fix                                  | When it applies                                    |
| ------------------------------------ | -------------------------------------------------- |
| Extract shared code to a third module | Both depend on the same constant or type          |
| Apply [dependency inversion](./Dependency%20inversion%20principle.md) | A low-level module calls back into a high-level one |
| Publish an event                     | One module only needs to notify another            |
| Pass a value as a parameter          | A function needs one value from the other module   |
| Merge the modules                    | They are really one concept                        |

Detect cycles with tools such as `madge`, `dependency-cruiser` or the ESLint `import/no-cycle` rule, and run them in CI, where the check acts as a [fitness function](./Fitness%20function.md). Moving an import inside a function avoids the load-order error but leaves the dependency in place.

_Usage:_

"Tests crash with 'Class extends value undefined', but only when run alone."

"That's an import cycle between `order` and `customer`. Move the shared base class into its own module."
