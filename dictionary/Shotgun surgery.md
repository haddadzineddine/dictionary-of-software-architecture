---
description: A code smell where one logical change forces many small edits across many classes or files.
---

Shotgun surgery is a code smell in which one logical change forces many small edits across many classes or files. Martin Fowler and Kent Beck listed it in _Refactoring_ (1999). A typical case is adding a payment method and having to touch the checkout form, API validator, fee calculation, receipt template, report export and admin filter. The bug report after release concerns the one place that was missed.

```typescript
// Before: each file holds its own knowledge of payment methods.
const checkoutOptions = ["card", "paypal"]; // checkout.ts
const isValid = (m: string) => m === "card" || m === "paypal"; // api.ts
const feeRate = (m: string) => (m === "card" ? 0.029 : 0.034); // pricing.ts

// After: one definition that every file reads.
const paymentMethods = {
  card: { label: "Card", feeRate: 0.029 },
  paypal: { label: "PayPal", feeRate: 0.034 },
} as const;

type PaymentMethod = keyof typeof paymentMethods;
```

The cause is one decision spread across many modules, which is a form of low [cohesion](./Cohesion.md). Often the same knowledge has been duplicated, so [DRY](./DRY.md) applies. Layering can cause it too: in a strict layered architecture, adding one field may mean editing a controller, data object, service, repository and mapper. [Package by feature](./Package%20by%20feature.md) and [vertical slice architecture](./Vertical%20slice%20architecture.md) reduce this by keeping code that changes together in one place.

To fix it, move the scattered pieces of the decision into one module. Where behaviour varies by type, use a lookup table or the [strategy pattern](./Strategy%20pattern.md). When full consolidation is not sensible, make the compiler find the sites: a value typed `Record<PaymentMethod, Rate>` fails to compile until each method has an entry, which turns a forgotten edit into a build error.

_Refactoring_ pairs this smell with divergent change, its mirror image. Divergent change is one class edited for many unrelated reasons, as seen in a [god object](./God%20object.md). Shotgun surgery is one reason requiring edits to many classes.

Some wide changes are legitimate. Renaming a shared API field touches every caller once and does not indicate a design problem. The smell is the same kind of change fanning out repeatedly.

_Usage:_

"We added the new payment method and refunds broke."

"Refunds had their own copy of the list. That's the sixth file for one change. Let's define the methods in one place."
