---
description: "You aren't gonna need it: do not build a capability until a real, current requirement calls for it."
---

YAGNI stands for "you aren't gonna need it", a practice from Extreme Programming: do not build a capability until a current requirement calls for it.

The symptom is code that exists for a future that never arrived. A `StorageProvider` interface has one implementation, a config option has never been set to anything but its default, and a tenant column holds `1` in every row. Each of these still has to be read, tested and worked around, and later changes take longer because of them. The resulting smell is called [speculative generality](./Speculative%20generality.md).

A speculative feature costs more than the time to build it:

| Cost        | What happens                                                  |
| ----------- | ------------------------------------------------------------- |
| Build       | Time is taken from work with a known need                     |
| Delay       | Needed features ship later                                    |
| Carry       | Every later change must accommodate the extra code            |
| Wrong guess | The real need differs from the guess, so the code is reworked |

YAGNI depends on code being cheap to change later. Tests, clear module boundaries and regular refactoring are what make it safe to defer work. Without them, deferral turns into [technical debt](./Technical%20debt.md) rather than saved effort.

The practice applies to features and speculative flexibility, not to basic quality. Error handling, tests and readable names are part of building the current requirement. Some decisions are also expensive to reverse, such as public API shapes, data formats, identifiers and security models, and those justify more thought up front. The idea of the [last responsible moment](./Last%20responsible%20moment.md) helps here: delay a decision until the cost of waiting exceeds the cost of deciding.

A practical check is to ask what it would cost to add the capability when it is needed. If the cost is about the same as now, wait. If it would require migrating every customer's data, decide now.

_Usage:_

"Should we make the notifier pluggable in case we add SMS?"

"Nobody has asked for SMS. Call the email service directly, and extract an interface if SMS actually comes up."
