---
description: A place where behaviour can be changed without editing the code at that place, often used to test legacy code.
---

A seam is a place in a program where behaviour can be changed without editing the code at that place. Michael Feathers defined the term in _Working Effectively with Legacy Code_, where seams are the means of getting untested code under test. Each seam has an enabling point, the place where you decide which behaviour is used.

The problem a seam solves is code you cannot test without triggering its side effects. A function charges a real card, sends a real email or reads the system clock, so the only way to exercise it is to run it for real, and it goes unrefactored because nobody can check the result.

```typescript
// No seam: the client and the clock are fixed inside the function
async function renewSubscription(id: string) {
  const sub = await stripe.subscriptions.retrieve(id);
  if (sub.endsAt < Date.now()) await stripe.invoices.create({ subscription: id });
}

// Seam: the parameters are the enabling point
async function renewSubscription(id: string, billing: Billing, now: () => number) {
  const sub = await billing.getSubscription(id);
  if (sub.endsAt < now()) await billing.invoice(id);
}
```

Feathers describes three kinds:

| Seam          | Enabling point                  | TypeScript example                       |
| ------------- | ------------------------------- | ---------------------------------------- |
| Object        | Which object is passed in       | A constructor or function parameter      |
| Link          | What is resolved at load time   | `vi.mock("./billing")`                   |
| Preprocessing | Substitution before compilation | A bundler's `define` replacing a constant |

Object seams are generally preferable because they are explicit in the signature. Module mocks need no change to the code, but they depend on file paths and can break when files move.

Seams are also useful outside tests. A feature flag, an [adapter](./Adapter%20pattern.md) or a [strategy](./Strategy%20pattern.md) is a seam for switching behaviour, and a strangler fig migration relies on a seam where traffic can be redirected.

Introduce a seam where you need to vary behaviour, often at the boundary with an external system. Adding one around every function adds parameters and indirection without benefit. In legacy code, make the smallest change that creates a seam, add tests around the behaviour, and then refactor.

_Usage:_

"I can't test renewals without hitting Stripe."

"Add a seam. Pass the billing client in as a parameter and give the test a fake."
