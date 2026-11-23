---
description: Code made flexible for future needs that never arrive, leaving hooks and parameters with only one real use.
---

Speculative generality is code made flexible for future needs that have not arrived. Martin Fowler and Kent Beck listed it as a code smell in _Refactoring_ (1999). It is recognisable by interfaces with one implementation, parameters that every caller sets to the same value, abstract classes with one subclass, and plugin systems with one plugin. The felt symptom is tracing a one-line change through a factory, a provider and a strategy, then finding that only one path exists.

```typescript
// Built for many channels. Only email has ever existed.
interface NotificationChannel<TPayload, TOptions> {
  send(payload: TPayload, options?: TOptions): Promise<void>;
}

class NotificationChannelFactory {
  create(type: "email"): NotificationChannel<EmailPayload, EmailOptions> {
    return new EmailChannel();
  }
}

// What every caller needs.
async function sendEmail(to: string, subject: string, body: string) {}
```

The extra code must be read, tested and maintained from the day it is written. The prediction is also often wrong, so when the second case arrives it does not fit the prepared shape and the structure has to be reworked anyway. [YAGNI](./YAGNI.md) is the principle that addresses this directly.

Some flexibility is justified, and the cost of changing later is the deciding factor:

| Flexibility                         | Justified when                                         |
| ----------------------------------- | ------------------------------------------------------ |
| Interface with one production class | Tests use a second implementation, or the vendor may change |
| Extension point in a public library | Later changes would break consumers you do not control |
| Extra care in a data format         | Migrating stored data would be expensive               |
| Options on an internal helper       | Rarely; add them when a caller needs them              |

Decisions that are cheap to reverse can wait until the [last responsible moment](./Last%20responsible%20moment.md).

This smell differs from [premature abstraction](./Premature%20abstraction.md). Premature abstraction merges existing code too early because it looks similar. Speculative generality adds capability for cases that do not exist.

To remove it, inline the single implementation, delete unused parameters and collapse hierarchies with one subclass. Version control keeps the old design if the need ever appears.

_Usage:_

"What does `NotificationChannelFactory` support?"

"Email. It has only ever supported email. Let's replace it with one function and add a second channel when we need one."
