---
description: The gradual divergence between a system's intended architecture and the one actually implemented in code.
---

Architectural drift is the gradual divergence between a system's intended architecture and the structure actually present in its code. It usually happens through many small, locally reasonable changes rather than one bad decision.

The usual symptom is a diagram that no longer matches the system. The document shows controllers calling services and services calling repositories, but a new engineer finds controllers running SQL directly and two supposedly independent modules importing each other. Estimates grow, because the real dependencies stay invisible until a change breaks something.

Drift comes from deadline shortcuts, staff turnover and rules that exist only in people's heads. Coding agents can accelerate it, because they tend to copy whichever pattern they find nearby, including a violation.

| Term    | Meaning                                                     | Example                                                  |
| ------- | ----------------------------------------------------------- | -------------------------------------------------------- |
| Drift   | Code departs from the design's intent without breaking a stated rule | A utility module slowly accumulates business logic |
| Erosion | Code violates an explicit architectural constraint          | The UI imports the database client despite a layering rule |

Some authors use the two terms interchangeably.

Detect drift by comparing the design with the code. Dependency analysis tools show the actual import graph, and change history shows modules that always change together. A [fitness function](./Fitness%20function.md) that checks allowed dependencies can then stop new violations in CI.

Each gap needs a decision, because the code is not always the wrong side. If the code reflects a better understanding of the domain, update the diagram and record the change in an [architecture decision record](./Architecture%20decision%20record.md). If it is an accidental violation, fix it, or log it as [technical debt](./Technical%20debt.md) with an owner. Left unmanaged for years, drift tends toward a [big ball of mud](./Big%20ball%20of%20mud.md).

_Usage:_

"The diagram says billing only talks to orders through its API."

"It did two years ago. Billing now reads the orders table directly in four places."
