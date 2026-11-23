---
description: An object that wraps access to an external system behind an interface owned by the application.
---

The gateway pattern wraps access to an external system or resource in an object whose interface is owned by the application. Code calls `payments.charge(amount, token)` instead of using a vendor SDK or building HTTP requests. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002).

```typescript
interface PaymentGateway {
  charge(amount: Money, token: string): Promise<ChargeResult>;
}

class StripeGateway implements PaymentGateway {
  constructor(private stripe: Stripe) {}

  async charge(amount: Money, token: string) {
    const intent = await this.stripe.paymentIntents.create({
      amount: amount.cents,
      currency: amount.currency,
      payment_method: token,
      confirm: true,
    });
    return { id: intent.id, succeeded: intent.status === "succeeded" };
  }
}
```

The pattern addresses external details spreading across a codebase. When a payment SDK is imported in forty files, a major version upgrade touches all of them, changing vendor becomes a project, and every test that reaches that code needs network access or an elaborate mock. With a gateway, the SDK appears in one class. Tests substitute an in-memory implementation at this [seam](./Seam.md), and retries, timeouts and error translation have one home.

A useful gateway interface uses the application's vocabulary and returns its types. If `charge` returns a raw Stripe object, callers still depend on Stripe, which makes the wrapper a [leaky abstraction](./Leaky%20abstraction.md). Translate vendor errors into a small set of meaningful failures, such as `CardDeclined`.

| Pattern                                              | Purpose                                 | Scope                |
| ---------------------------------------------------- | --------------------------------------- | -------------------- |
| Gateway                                              | Wraps access to an external system      | One outside resource |
| [Adapter](./Adapter%20pattern.md)                    | Converts one interface to another       | Any two interfaces   |
| [Facade](./Facade%20pattern.md)                      | Simplifies a complicated subsystem      | Often internal       |
| [Anti-corruption layer](./Anti-corruption%20layer.md) | Protects a model from a foreign one     | A whole integration  |

The name overlaps with API gateway, a separate piece of infrastructure that routes network requests to backend services. A gateway in this sense is an in-process class. It is also commonly implemented with an adapter, so both labels can apply to the same code. Skip the wrapper for stable platform features that tests have no need to replace, such as a standard-library function.

_Usage:_

"Upgrading the Stripe SDK changed 38 files."

"Every feature calls it directly. Add a `PaymentGateway` and move the SDK behind it as part of this upgrade."
