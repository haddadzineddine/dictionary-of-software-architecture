---
description: A method should either change state or return data, but not both, so reading a value never causes a side effect.
---

Command-query separation is the rule that a method should either be a command, which changes state and returns nothing, or a query, which returns data and changes nothing. Bertrand Meyer defined it in his work on the Eiffel language and in _Object-Oriented Software Construction_.

The symptom is a bug caused by a call that looks like a read. A developer adds a `getUser()` call to a log statement and the system starts misbehaving, because `getUser()` also creates the user if missing or increments a login counter. Logging, retrying or reordering the call now changes behaviour.

```typescript
// Mixed: looks like a read, but writes
function getNextInvoiceNumber(): number {
  return ++counter;
}

// Separated
function currentInvoiceNumber(): number {
  return counter;
}

function advanceInvoiceNumber(): void {
  counter += 1;
}
```

Queries that follow the rule are safe to call repeatedly, cache, log and reorder, so a reader can reason about them without tracing into their bodies. A getter with a hidden write breaks the [principle of least astonishment](./Principle%20of%20least%20astonishment.md). Commands fit [tell don't ask](./Tell%20don't%20ask.md), where callers instruct an object and do not inspect its state first.

There are legitimate exceptions, mostly where a read and a write must happen atomically:

| Operation                   | Why it mixes both                             |
| --------------------------- | --------------------------------------------- |
| `stack.pop()`               | Removes and returns in one step               |
| `INSERT ... RETURNING id`   | The caller needs the generated key            |
| `counter.incrementAndGet()` | Separate calls would race                     |
| Compare-and-swap            | The check and the write must be one operation |

The invoice example above shows the risk. With concurrent callers, two requests can read the same number before either advances it, so a real invoice counter needs one atomic operation. Follow the rule by default, and when it must be broken, name the method so the side effect is visible, such as `claimNextInvoiceNumber()`.

Command-query separation is different from CQRS. This rule applies to a single method or object. CQRS applies the same split at the architectural level, with separate models, and sometimes separate data stores, for reads and writes. A codebase can follow one without the other.

_Usage:_

"Adding a debug log changed the test results."

"The log calls `getSession()`, and that refreshes the expiry. Split it into a read and an explicit `refreshSession()`."
