---
description: A common response to a recurring problem that looks reasonable but produces worse results than a known alternative.
---

An anti-pattern is a common response to a recurring problem that looks reasonable but produces worse results than a known alternative. The definition has two parts: the approach is widespread enough to deserve a name, and a better option exists. A one-off mistake is a bug, and a poor option with no better alternative is a constraint. The 1998 book _AntiPatterns_ by Brown, Malveau, McCormick and Mowbray popularised the term by cataloguing these approaches in a format similar to design patterns.

Anti-patterns persist because their early costs are low and their later costs often fall on someone else. Adding one more method to a [god object](./God%20object.md) is the quickest way to finish today's ticket. The team usually notices the result months later, when small changes take days and nobody can predict what a release will break.

The term is often confused with nearby vocabulary:

| Term                                    | What it describes                           | Typical response                    |
| --------------------------------------- | ------------------------------------------- | ----------------------------------- |
| Bug                                     | Behaviour that is wrong                     | Fix it                              |
| Code smell                              | A surface sign that may indicate a problem  | Investigate                         |
| Anti-pattern                            | A recurring approach that causes harm       | Replace it with the known alternative |
| [Technical debt](./Technical%20debt.md) | A cost accepted now and repaid later        | Schedule repayment or accept it     |

Some entries in this section, such as [shotgun surgery](./Shotgun%20surgery.md) and [feature envy](./Feature%20envy.md), began as code smells, a term Kent Beck coined for Martin Fowler's _Refactoring_ (1999). A smell is a prompt to look closer and does not prove that the design is wrong.

A shared name makes design review faster, because "this is turning into a [big ball of mud](./Big%20ball%20of%20mud.md)" conveys a known failure and its direction. The label is not an argument by itself. A [singleton](./Singleton.md) is called an anti-pattern by some engineers and is a reasonable choice for a process-wide logger. Before applying the label, state the specific cost the code imposes and the alternative you would use. If you cannot name both, treat the concern as a preference.

_Usage:_

"This handler queries the database directly. Isn't that an anti-pattern?"

"It's a forty-line internal script with one query. What would the alternative save us?"
