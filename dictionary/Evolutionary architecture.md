---
description: An approach to architecture that supports guided, incremental change, using automated checks to protect chosen qualities.
---

Evolutionary architecture is an approach that designs a system to support guided, incremental change over time. Neal Ford, Rebecca Parsons and Patrick Kua set it out in _Building Evolutionary Architectures_ (2017).

The approach responds to requirements, tools and scale changing in ways nobody can predict at the start. A design fixed up front tends to fit the first version of the product and resist later ones. Teams then experience a familiar cycle: the system grows harder to change until a rewrite is proposed, and the rewrite starts the same cycle.

| Element                                    | What it means                                  | Example                               |
| ------------------------------------------ | ---------------------------------------------- | ------------------------------------- |
| Incremental change                         | Small, frequent, reversible changes            | Continuous delivery, feature flags    |
| [Fitness functions](./Fitness%20function.md) | Automated checks protecting chosen qualities   | Build fails on a forbidden dependency |
| Appropriate [coupling](./Coupling.md)      | Boundaries that let parts change independently | Modules with explicit contracts       |

The method pairs freedom to change with automated guardrails. A team can replace a component or reshape a module because its fitness functions show whether performance, security and structure are still acceptable. Without these checks, incremental change is unguided and tends to produce [architectural drift](./Architectural%20drift.md).

Evolutionary architecture is not the absence of design. Teams still make and record structural decisions, but they defer irreversible ones to the [last responsible moment](./Last%20responsible%20moment.md) and prefer choices that are cheap to undo. A large migration proceeds in stages, for example using a strangler fig to replace one route at a time while the old system serves the rest.

The approach has costs. It depends on a reliable delivery pipeline, good test coverage and time to maintain the checks, and a team that deploys quarterly cannot evolve in small steps. Some decisions, such as a public API or a data model shared with partners, remain expensive however the system is built, so they warrant more care up front. For a short-lived or stable system, the investment may not pay off.

_Usage:_

"We keep saying the next rewrite will finally get the structure right."

"Let's stop betting on a rewrite. Add checks for the boundaries we care about and move one module at a time."
