---
description: Replacing a null reference with an object that has the same interface and deliberately does nothing.
---

The null object pattern replaces a missing collaborator with an object that implements the same interface and does nothing, or returns a neutral value. Callers use it like any other implementation and do not check for absence. It is not one of the 23 patterns in the Gang of Four book.

```typescript
interface Logger {
  info(message: string): void;
}

class ConsoleLogger implements Logger {
  info(message: string) {
    console.log(message);
  }
}

class NullLogger implements Logger {
  info() {}
}

class ImportJob {
  constructor(private logger: Logger = new NullLogger()) {}

  run() {
    this.logger.info("starting");
  }
}
```

The pattern addresses optional dependencies that force a check at each use. Code fills with `if (logger) logger.info(...)`, and the one call that omits the check crashes with `Cannot read properties of undefined`, often in an error path that rarely runs. A null object removes those branches because there is always a valid object to call. Neutral values work the same way: an empty list, a zero discount or a guest user whose permissions are all false.

The main danger is hiding a real failure. A silent logger is harmless. A `NullPaymentGateway` used because a production config key is missing means orders are marked paid with no charge, and nothing raises an error. Use the pattern only when doing nothing is a correct outcome for the business. If absence means something is wrong, fail at startup or throw.

| Situation                                   | Better choice                  |
| ------------------------------------------- | ------------------------------ |
| Optional logging, metrics or tracing        | Null object                    |
| Empty collection                            | Return an empty array          |
| Record not found, and the caller must react | Return `null` or a result type |
| Required dependency is missing              | Fail at startup                |

In TypeScript with `strictNullChecks`, the compiler already forces callers to handle `null`, and optional chaining such as `logger?.info()` is short. That lowers the need for this pattern in small cases.

A null object differs from a test stub, even though both can be empty classes. A stub exists for tests, while a null object is a legitimate production behaviour. It is often a [strategy](./Strategy%20pattern.md) that performs no work. It honours the [Liskov substitution principle](./Liskov%20substitution%20principle.md) only if callers do not depend on the action having taken place.

_Usage:_

"Orders were marked paid all weekend with no charges in Stripe."

"The missing key fell back to `NullPaymentGateway`. Payments must fail at startup instead of doing nothing."
