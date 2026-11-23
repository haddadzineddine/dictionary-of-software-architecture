---
description: A system made so configurable that it becomes a poor copy of the platform it runs on.
---

The inner-platform effect is the tendency of a configurable system to grow into a poor copy of the platform it runs on. A table of generic `entity`, `attribute` and `value` rows rebuilds a database inside a database. A rules engine that gains conditions, variables and loops becomes a programming language with no debugger, tests or version control. The symptoms are a simple report that needs six self-joins, a configuration edit that takes down production and cannot be diffed, and a "no-code" tool that only one engineer can safely change.

| Inner platform                     | What it re-creates   | What is lost                               |
| ---------------------------------- | -------------------- | ------------------------------------------ |
| Entity-attribute-value tables      | Database schema      | Types, constraints, indexes, simple queries |
| YAML with conditions and loops     | Programming language | Type checking, debugger, tests             |
| Visual workflow builder            | Application code     | Diffs, code review, rollback               |
| Custom query language over SQL     | SQL                  | Query features, documentation, tooling     |
| Windowing system inside a web page | Browser or OS        | Accessibility, standard keyboard behaviour |

The effect develops through reasonable steps. To avoid a deployment, a team makes a value configurable. A later request needs a condition, and another needs a variable. Eventually the configuration requires an engineer to write it, and that engineer has fewer tools than the host language provided. The original motive is often [speculative generality](./Speculative%20generality.md) or a wish to let non-engineers make changes.

Prefer the platform's own features first. Limit configuration to values, and keep logic in code. If the reason for configuration is that deployment is slow, fixing deployment usually removes the need for it.

Some products do need an extension layer. A multi-tenant product where customers define their own fields needs some metadata model, and a [plugin architecture](./Plugin%20architecture.md) or the [interpreter pattern](./Interpreter%20pattern.md) can suit users outside the team who must extend the system. In those cases, treat the inner platform as a product, with validation, tests, versioning and documentation, and keep its scope deliberately small.

_Usage:_

"Can you change the discount rule in the workflow builder?"

"Nobody can debug it now that it has loops and variables. Let's move this rule back to code and ship it through CI."
