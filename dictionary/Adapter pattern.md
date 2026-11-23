---
description: A wrapper that converts one interface into the interface a caller expects, so incompatible code can work together.
---

The adapter pattern wraps an object and translates its interface into the one a caller expects. It is a structural pattern from the Gang of Four book (1994). The adapter holds the incompatible object and maps each call, argument and result between the two shapes.

```typescript
interface PaymentGateway {
  charge(amountCents: number, customerId: string): Promise<{ id: string }>;
}

class StripeAdapter implements PaymentGateway {
  constructor(private stripe: Stripe) {}

  async charge(amountCents: number, customerId: string) {
    const intent = await this.stripe.paymentIntents.create({
      amount: amountCents,
      currency: "usd",
      customer: customerId,
    });
    return { id: intent.id };
  }
}
```

The pattern is used when one side of a call cannot change, usually because it is a third-party SDK. Without an adapter, vendor types spread through business logic. When the vendor ships a breaking version or the company switches provider, the change touches dozens of files instead of one class. An adapter confines that vendor knowledge and gives tests a [seam](./Seam.md) where a fake can replace the real client.

Translation must include failure modes as well as method names. If vendor-specific errors escape the adapter, callers end up catching `StripeCardError`, which is a [leaky abstraction](./Leaky%20abstraction.md). Map errors to types your application defines. Units, date formats and null handling are other sources of quiet bugs, such as a provider that expects dollars when you send cents.

The structural patterns that wrap an object are often confused:

| Pattern                               | Interface offered                 | Purpose                    |
| ------------------------------------- | --------------------------------- | -------------------------- |
| Adapter                               | Different from the wrapped object | Make incompatible code fit |
| [Decorator](./Decorator%20pattern.md) | Same                              | Add behaviour              |
| [Proxy](./Proxy%20pattern.md)         | Same                              | Control access             |
| [Facade](./Facade%20pattern.md)       | New, simpler                      | Hide a subsystem           |

Between systems, an [anti-corruption layer](./Anti-corruption%20layer.md) uses adapters to keep another system's model from entering your own.

Skip the adapter when the dependency is stable, used in one place and already matches your needs. A pass-through class adds a file without isolating anything.

_Usage:_

"Upgrading the Stripe SDK broke forty files."

"Its types are used everywhere. Put it behind a `PaymentGateway` adapter so the next upgrade touches one class."
