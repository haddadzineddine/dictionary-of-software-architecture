---
description: A condition that must always hold for an object or system, such as an order total matching its lines.
---

An invariant is a condition that must always be true for an object or system whenever its state can be observed. Examples are an order's total equalling the sum of its lines, an account balance staying above its overdraft limit, and a booking's end date falling after its start date.

Broken invariants appear as data that should be impossible. Support finds an order with no lines, a refund larger than the original payment, or a subscription that is both active and cancelled. Developers respond by adding defensive checks such as `if (order.lines.length === 0)` throughout the code, because they can no longer trust the data. The usual cause is that several code paths write the same state and one skips a rule.

Invariants differ from input validation. Validation checks whether a request is acceptable and can reject it with a message, such as a malformed email. An invariant describes what must hold for an object's state regardless of how the change was requested. Validation runs at the boundary, while the model enforces the invariant for every path, including imports, scripts and background jobs.

| Enforcement                  | Example                                     | Coverage                     |
| ---------------------------- | ------------------------------------------- | ---------------------------- |
| Type system                  | `NonEmptyArray<OrderLine>` rules out no lines | Compile time               |
| Constructor                  | `Money.of` rejects a fractional cent        | Every instance               |
| [Aggregate](./Aggregate.md) root | `addLine` checks the credit limit       | Every change via the root    |
| Database constraint          | `CHECK (ends_at > starts_at)`, unique index | Every write, including raw SQL |
| Reconciliation job           | Nightly comparison of ledger and payments   | Detects violations afterwards |

Prefer the earliest level that can express the rule. Keep fields private so that [encapsulation](./Encapsulation.md) stops code from bypassing the check, and add a database constraint for rules that must survive scripts and migrations.

Invariants that span several aggregates cannot normally be kept within one transaction. Such rules are usually relaxed to eventual consistency, with compensating actions or reconciliation. Ask the business how long a violation can be tolerated, because the answer often changes where the aggregate boundary is drawn.

_Usage:_

"How did a refund end up larger than the payment?"

"The admin script writes refunds directly. Put that invariant on `Payment.refund` and add a database constraint."
