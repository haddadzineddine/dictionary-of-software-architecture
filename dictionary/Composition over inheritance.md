---
description: Building behaviour by combining objects instead of extending classes, which avoids rigid and fragile class hierarchies.
---

Composition over inheritance is the guideline to build behaviour by holding and delegating to other objects instead of extending a parent class. The Gang of Four book (1994) stated it as "favor object composition over class inheritance".

The symptom is a class hierarchy that multiplies. A `Notification` class gains `EmailNotification` and `SmsNotification`, then someone needs retries and urgency, producing `RetryingUrgentEmailNotification`. Changing a method in the base class can also break subclasses that relied on its internals, a problem known as the fragile base class.

```typescript
interface Channel {
  send(message: string): Promise<void>;
}

class Retrying implements Channel {
  constructor(private inner: Channel, private attempts: number) {}

  async send(message: string) {
    for (let i = 1; ; i++) {
      try {
        return await this.inner.send(message);
      } catch (error) {
        if (i >= this.attempts) throw error;
      }
    }
  }
}

const channel = new Retrying(new EmailChannel(), 3);
```

Each behaviour is now a small object, and combinations are assembled at runtime instead of declared as classes. The [decorator](./Decorator%20pattern.md) and [strategy](./Strategy%20pattern.md) patterns both work this way.

|                      | Inheritance                          | Composition                 |
| -------------------- | ------------------------------------ | --------------------------- |
| Relationship         | Is a                                 | Has a, uses a               |
| Binding              | Fixed at compile time                | Can change at runtime       |
| Access to internals  | Subclass sees protected state        | Only the public interface   |
| Combining behaviours | One parent, so combinations multiply | Any combination             |
| Boilerplate          | Methods inherited for free           | Forwarding may be needed    |

The guideline says "over", not "instead of". Inheritance fits when there is a true subtype relationship that satisfies the [Liskov substitution principle](./Liskov%20substitution%20principle.md), the hierarchy is shallow, and the base class is designed to be extended, as in the [template method](./Template%20method.md) pattern. Composition has its own costs: more small objects, forwarding code, and behaviour spread across the wiring rather than visible in one class.

_Usage:_

"We need an urgent version of `RetryingEmailNotification`."

"That's a third level of subclass. Make retry and urgency wrappers around a `Channel` and combine them."
