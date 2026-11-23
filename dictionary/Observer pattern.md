---
description: Letting objects subscribe to a subject and be notified automatically whenever its state changes.
---

The observer pattern lets objects subscribe to a subject and receive a notification when the subject changes. It is a behavioural pattern from the Gang of Four book (1994). The subject keeps a list of observers and calls each one, without knowing what they do.

```typescript
type Listener<T> = (value: T) => void;

class Subject<T> {
  private listeners = new Set<Listener<T>>();

  subscribe(listener: Listener<T>) {
    this.listeners.add(listener);
    return () => this.listeners.delete(listener);
  }

  emit(value: T) {
    for (const listener of this.listeners) listener(value);
  }
}
```

The pattern lets a change in one module trigger behaviour in others without the first module importing them. An order module can emit `orderPlaced`, and email, analytics and inventory can each subscribe, which reduces [coupling](./Coupling.md) and lets new reactions be added without editing the subject. DOM events, Node's `EventEmitter` and reactive UI libraries all use it.

The pattern has several recurring failures:

| Failure               | Symptom                                                            | What to do                                 |
| --------------------- | ------------------------------------------------------------------ | ------------------------------------------ |
| Forgotten unsubscribe | Memory grows, Node prints `MaxListenersExceededWarning`            | Return and call a cleanup function         |
| Listener throws       | Later listeners never run, and the emitter's caller sees the error | Catch per listener where isolation matters |
| Cascading updates     | One change triggers a chain of notifications or an infinite loop   | Avoid emitting from inside a listener      |

Observers also hide control flow. Reading `order.place()` does not reveal what runs afterwards, so a slow listener can delay the request with no visible cause in the calling code. Log or trace listeners.

In-process observers are not durable. If the process crashes after the database commit but before a listener finishes, that work is lost. For work that must happen, such as sending a receipt, use a persisted approach such as the outbox pattern.

The observer differs from publish-subscribe. An observer subject holds direct references to its subscribers in one process. Publish-subscribe places a broker between them, so neither side knows the other and the two can run on separate machines. A [mediator](./Mediator%20pattern.md) differs in that it holds coordination logic, whereas a subject only announces a change. A [domain event](./Domain%20event.md) is a common payload for this mechanism.

Use a direct call when one module must always invoke exactly one other.

_Usage:_

"Memory climbs every time someone opens and closes the chat panel."

"The panel subscribes on mount and never unsubscribes. Return a cleanup function from the effect."
