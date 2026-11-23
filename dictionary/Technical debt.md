---
description: The future cost of choosing a faster or less complete approach now, paid as slower and riskier changes later.
---

Technical debt is the future cost created by leaving code or design in a state that makes later changes slower or riskier. Ward Cunningham introduced the metaphor in 1992: shipping before the design fully reflects your understanding is like borrowing money, and the extra effort on each later change is the interest.

The symptom is delivery that slows while the team stays the same size. Features that took days now take weeks, engineers avoid a particular module, and fixing one bug produces another. The principal is the work needed to fix the design. The interest is paid whenever someone has to work around it.

Debt has different causes. Martin Fowler's technical debt quadrant separates four kinds:

|             | Reckless                        | Prudent                                       |
| ----------- | ------------------------------- | --------------------------------------------- |
| Deliberate  | "We don't have time for design" | "We must ship now and deal with consequences" |
| Inadvertent | "What's Layering?"              | "Now we know how we should have done it"      |

Deliberate, prudent debt can be a sound [architectural trade-off](./Architectural%20trade-off.md), for example hard-coding a tax rate to test a market before building a tax engine. It stays sound only if someone records it and returns to it. Cunningham's original meaning was closer to the bottom right: code written with the understanding available at the time, then refactored as understanding improves. Code that is simply careless is a different problem, and calling it debt can hide that.

Manage debt according to where it charges interest. Code that is ugly but stable costs little. Code that changes weekly and is hard to change costs a lot, so prioritise by combining change frequency with difficulty. Pay down debt as part of feature work in the affected area, and track larger items with an owner and a stated cost. A full rewrite carries its own risks, so prefer incremental replacement.

_Usage:_

"Why does every change to invoicing take a week?"

"We hard-coded the tax logic for launch and never went back. We're paying interest on it now."
