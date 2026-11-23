---
description: A central registry that code asks for its dependencies at runtime, which hides what each class actually needs.
---

A service locator is a central registry that code calls at runtime to obtain its dependencies. Instead of receiving a logger or a database client, a class asks for one with something like `locator.get("db")`. It solves the problem of reaching shared services from deep in a call stack without passing them through every layer, and it is one way to achieve [inversion of control](./Inversion%20of%20control.md).

```typescript
const locator = new Map<string, unknown>();
locator.set("mailer", new SmtpMailer());

class InvoiceService {
  send(invoice: Invoice) {
    const mailer = locator.get("mailer") as Mailer;
    return mailer.deliver(invoice);
  }
}
```

The main criticism is that dependencies become invisible. The signature of `InvoiceService` shows no need for a mailer, so the failure appears at runtime: a test or new entry point crashes with "service not registered" because something deep in the call chain asked for a service nobody set up. Tests must configure shared state and can interfere with each other. Some authors, including Mark Seemann, classify it as an [anti-pattern](./Anti-pattern.md) for application code.

It differs from dependency injection in how the dependency arrives:

|                       | Service locator          | Dependency injection    |
| --------------------- | ------------------------ | ----------------------- |
| How code gets it      | Asks for it              | Receives it             |
| Visible in signature  | No                       | Yes                     |
| Missing one is found  | When the line runs       | At startup or compile time |
| Test setup            | Register in a registry   | Pass a fake             |
| Wiring effort         | Low                      | Passing through layers  |

The pattern still has legitimate uses. Plugin hosts often cannot know every service at compile time, and legacy code may need a way to reach a dependency without changing hundreds of signatures. React context is a related, scoped form, where a component reads a value provided higher in the tree.

Prefer constructor or function parameters in new code. If a locator is necessary, restrict calls to the outermost layer, such as a request handler, and pass resolved objects inward. This stops the locator growing into a global access path and a source of hidden [coupling](./Coupling.md).

_Usage:_

"This test crashes with 'mailer not registered', but the class doesn't mention a mailer."

"It pulls one from the service locator. Pass the mailer to the constructor so the dependency is visible."
