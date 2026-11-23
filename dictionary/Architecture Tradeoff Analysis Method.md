---
description: A structured SEI review that evaluates an architecture against prioritised quality scenarios to expose risks and trade-offs.
---

The Architecture Tradeoff Analysis Method (ATAM) is a structured review for evaluating a software design against its [quality attribute](./Quality%20attribute.md) goals. It was developed at the Software Engineering Institute at Carnegie Mellon University. An evaluation team works with architects and stakeholders to find where a design puts those goals at risk, before the cost of changing it grows.

ATAM suits major commitments where a late structural flaw would be expensive, such as a multi-year platform. The failure it guards against is discovering at acceptance testing that an approved design cannot meet its throughput or failover requirements, after the budget has been spent building it.

| Phase                 | Who                                | What happens                                                        |
| --------------------- | ---------------------------------- | ------------------------------------------------------------------- |
| 0. Preparation        | Evaluation and project leaders     | Agree scope, logistics and participants                             |
| 1. Evaluation         | Evaluators, architects, project leads | Present drivers and design, build a utility tree, analyse approaches |
| 2. Wider evaluation   | The above plus stakeholders        | Brainstorm and rank scenarios, analyse again, present results       |
| 3. Follow-up          | Evaluation team, sponsor           | Deliver the written report                                          |

The analysis produces specific findings rather than a pass or fail:

| Output            | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| Sensitivity point | A decision that strongly affects one quality               |
| Trade-off point   | A decision that affects several qualities in opposing ways |
| Risk              | A decision that may cause a problem                        |
| Non-risk          | A decision judged safe, with the reasons                   |
| Risk theme        | A pattern across risks, tied to business drivers           |

ATAM is costly, because it involves many people over several days plus preparation. Most product teams do not need the full method. A lighter version keeps the useful parts: write the top five scenarios, walk the design through each, and capture each [architectural trade-off](./Architectural%20trade-off.md) in an [architecture decision record](./Architecture%20decision%20record.md). ATAM evaluates a design but does not produce one, and it does not replace measuring the built system.

_Usage:_

"We're committing three years of budget to this platform design. How do we test it on paper?"

"Run an ATAM with the stakeholders, or at least walk the top failover scenarios through the design."
