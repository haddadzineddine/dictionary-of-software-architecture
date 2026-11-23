---
description: A guideline to tell objects what to do instead of querying their state and making the decision for them outside.
---

Tell don't ask is the guideline that code should tell an object what to do, rather than asking for its state and making the decision outside it. Data and the rules that govern it stay in the same place.

The symptom is the same conditional appearing in several callers. The checkout, the admin panel and a background job each read `account.balance`, compare it to the amount and subtract. One of them forgets the overdraft rule, and accounts go negative.

```typescript
// Ask: the caller holds the rule
if (account.balance >= amount) {
  account.balance -= amount;
}

// Tell: the account holds the rule
account.withdraw(amount);

class Account {
  constructor(private balance: number) {}

  withdraw(amount: number) {
    if (amount > this.balance) throw new InsufficientFunds();
    this.balance -= amount;
  }
}
```

This protects an [invariant](./Invariant.md), because the balance can only change through a method that checks it, and it strengthens [encapsulation](./Encapsulation.md). Code that repeatedly pulls data out of another object to work on it shows [feature envy](./Feature%20envy.md). A model with only getters and setters, with all rules in services, is an [anemic domain model](./Anemic%20domain%20model.md).

Reading state remains normal and necessary in many places:

| Situation                              | Approach                                            |
| -------------------------------------- | --------------------------------------------------- |
| A rule about the object's own data     | Tell                                                |
| Showing data on a screen or a response | Ask                                                 |
| A decision spanning several objects    | Use a [domain service](./Domain%20service.md)       |
| Reports and queries                    | Read directly                                       |

Following the rule everywhere creates its own problem. If an `Order` gains `renderHtml()` and `toCsv()` so that nobody has to ask for its fields, it accumulates presentation concerns and moves toward a [god object](./God%20object.md). Keep business rules with the data, and let display code read what it needs.

Tell don't ask overlaps with the [Law of Demeter](./Law%20of%20Demeter.md), since both reduce how much callers know about another object's internals. Demeter limits which objects a method can talk to, while this guideline concerns where a decision lives.

_Usage:_

"Support found accounts with negative balances."

"Three places check the balance and subtract on their own. Move it into `account.withdraw()` so the rule exists once."
