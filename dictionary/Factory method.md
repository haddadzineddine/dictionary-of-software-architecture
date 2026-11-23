---
description: Defining a method that creates an object so subclasses decide which concrete class is produced.
---

The factory method pattern defines a method for creating an object and lets subclasses decide which concrete class to instantiate. It is one of the creational patterns in the Gang of Four book (1994). Code that needs the object calls the method and depends only on the returned interface.

```typescript
interface Notifier {
  send(to: string, body: string): Promise<void>;
}

abstract class AlertService {
  protected abstract createNotifier(): Notifier;

  async alert(to: string, body: string) {
    await this.createNotifier().send(to, body);
  }
}

class SmsAlertService extends AlertService {
  protected createNotifier() {
    return new SmsNotifier();
  }
}
```

The pattern addresses construction logic spread across call sites. When `new StripeClient(...)` appears in twenty files, or the same `switch (provider)` is copied wherever a client is needed, adding a provider means finding every copy, and a missed copy fails in production. Moving creation behind one method gives that decision a single home and supports the [open-closed principle](./Open-closed%20principle.md): a new variant adds a class, and the calling code stays unchanged.

In everyday TypeScript, the term is often used loosely for a plain function such as `createNotifier(config)`. That is a factory function, sometimes called a simple factory. It has no subclass hook, and it is usually the better choice, because inheritance adds [coupling](./Coupling.md) between parent and child. Reserve the class-based form for frameworks where a base class owns the workflow and subclasses supply one part. In that arrangement the factory method is often one step of a [template method](./Template%20method.md).

Factory method is often confused with [abstract factory](./Abstract%20factory.md). A factory method creates one product. An abstract factory is an object with several creation methods that produce a family of related products.

Skip the pattern when there is only one implementation and no realistic second one. A factory around a single constructor is [speculative generality](./Speculative%20generality.md): it adds a level of indirection that every reader must follow.

_Usage:_

"Adding PayPal means editing the provider switch in nine places."

"Move it into one `createPaymentClient` factory and have the nine call sites use that."
