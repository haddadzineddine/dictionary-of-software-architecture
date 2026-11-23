---
description: A vocabulary for coupling, where two parts are connascent if changing one requires changing the other to stay correct.
---

Connascence is a way of describing [coupling](./Coupling.md) precisely: two pieces of code are connascent if changing one requires changing the other to keep the system correct. Meilir Page-Jones introduced the term in the 1990s. It names the kind of dependency, so a reviewer can say more than "these are too coupled".

The forms run from weaker to stronger:

| Form      | Visible | Both sides must agree on | Example                             |
| --------- | ------- | ------------------------ | ----------------------------------- |
| Name      | Static  | A name                   | A method name at a call site        |
| Type      | Static  | A type                   | A parameter type                    |
| Meaning   | Static  | What a value means       | `status === 3` means shipped        |
| Position  | Static  | An order                 | `createUser("Ada", true, false)`    |
| Algorithm | Static  | A computation            | Client and server hash the same way |
| Execution | Dynamic | The order of calls       | `connect()` before `send()`         |
| Timing    | Dynamic | When things happen       | A `sleep(100)` waiting for a job    |
| Value     | Dynamic | Related values           | Two copies of a price must match    |
| Identity  | Dynamic | The same instance        | Two modules must share one object   |

Static forms are visible in source code, while dynamic forms appear only at runtime and are harder to find. The symptom of a strong form is a bug with no compile error. Someone swaps two boolean arguments or changes what status `3` means, and the code still type-checks while behaving incorrectly.

```typescript
// Connascence of position
createUser("Ada", true, false);

// Connascence of name
createUser({ name: "Ada", isAdmin: true, sendInvite: false });
```

Three properties decide how much a given connascence matters: strength is how hard it is to detect and change, locality is how far apart the two pieces are, and degree is how many places are involved.

The practical guidance is to refactor strong forms into weaker ones, such as replacing a magic number with a named constant, which converts connascence of meaning into connascence of name. Connascence of algorithm is often the duplication that [DRY](./DRY.md) targets. Keep the strong forms that remain close together, which also raises [cohesion](./Cohesion.md). Two functions in one file that rely on call order are acceptable, while the same reliance across two services is a risk.

_Usage:_

"Why did swapping those two booleans compile but break signup?"

"That's connascence of position. Use a named options object and the compiler will catch it."
