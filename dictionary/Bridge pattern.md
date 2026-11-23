---
description: Splitting an abstraction from its implementation so the two can vary independently through composition.
---

The bridge pattern splits a concept into two separate hierarchies, an abstraction and an implementation, and connects them through composition. It comes from the Gang of Four book (1994). Each side can then gain new variants without changing the other.

```typescript
interface MessageSender {
  send(to: string, text: string): Promise<void>;
}

class EmailSender implements MessageSender { /* ... */ }
class SlackSender implements MessageSender { /* ... */ }

abstract class Notification {
  constructor(protected sender: MessageSender) {}
  abstract notify(to: string): Promise<void>;
}

class PasswordReset extends Notification {
  notify(to: string) {
    return this.sender.send(to, "Reset your password");
  }
}

class InvoiceDue extends Notification {
  notify(to: string) {
    return this.sender.send(to, "Your invoice is due");
  }
}

new InvoiceDue(new SlackSender());
```

The pattern addresses class explosion, which appears when inheritance is used for two independent dimensions. Classes such as `EmailPasswordReset`, `SlackPasswordReset`, `EmailInvoiceDue` and `SlackInvoiceDue` multiply: three notification types across four channels need twelve classes, and adding one channel means writing three more. With a bridge, the same system has three plus four classes, and a new channel is one class. This applies [composition over inheritance](./Composition%20over%20inheritance.md).

"Implementation" in this pattern does not mean a concrete subclass of the abstraction. It means the lower-level operations that the abstraction delegates to. A drawing API over interchangeable platform back ends is a typical example.

The bridge is often confused with the [adapter](./Adapter%20pattern.md) and [strategy](./Strategy%20pattern.md) patterns.

| Pattern  | When applied         | Intent                                |
| -------- | -------------------- | ------------------------------------- |
| Bridge   | Designed up front    | Let two dimensions vary independently |
| Adapter  | Added after the fact | Make an existing interface fit        |
| Strategy | Designed up front    | Swap one algorithm inside an object   |

Code for bridge and strategy can look almost identical. The difference is scope: a strategy replaces one behaviour, while a bridge's implementation supports the abstraction's full set of operations.

Do not introduce a bridge for a dimension that has one variant. A single sender behind an interface is [speculative generality](./Speculative%20generality.md). Add the split when a second independent dimension exists.

_Usage:_

"Adding WhatsApp means writing a new class for all eight notification types."

"Channel and message type are separate dimensions. Bridge them so WhatsApp is one sender class."
