---
description: A document or diagram showing a system's bounded contexts and the relationships between them.
---

A context map is a document or diagram that shows the bounded contexts in a system and the relationships between them. Eric Evans introduced it in Domain-Driven Design (2003). Each relationship records which side depends on which, how their models translate, and how the teams coordinate.

The map makes hidden dependencies visible. Without one, a team renames a field in its event and learns from an incident that three other teams were consuming it. A context map shows who is upstream, whose changes flow to others, and who is downstream and absorbs them. It also shows where one word carries different meanings, so that each context keeps its own [ubiquitous language](./Ubiquitous%20language.md).

| Relationship                                          | Meaning                                               |
| ----------------------------------------------------- | ----------------------------------------------------- |
| Partnership                                           | Two teams plan and release dependent changes together |
| [Shared kernel](./Shared%20kernel.md)                 | Two contexts jointly own a small shared model         |
| Customer-supplier                                     | Upstream includes downstream's needs in its planning  |
| Conformist                                            | Downstream adopts upstream's model as it is           |
| [Anti-corruption layer](./Anti-corruption%20layer.md) | Downstream translates upstream's model into its own   |
| Open host service                                     | Upstream offers a defined protocol for many consumers |
| Published language                                    | Contexts exchange data in a documented shared format  |
| Separate ways                                         | Contexts do not integrate                             |

A map should describe the current situation, including the awkward parts. Drawing the intended architecture hides the problems the exercise is meant to find. If billing is in practice conformist to a vendor's data model, record that, because it shows where a vendor change will land.

The relationships are organisational as well as technical. A customer-supplier arrangement fails if the upstream team has no incentive to serve the downstream team, and [Conway's law](./Conway's%20law.md) means team boundaries tend to appear in the integration structure. [Team Topologies](./Team%20Topologies.md) offers a related vocabulary for how teams interact.

A context map differs from a container diagram in the [C4 model](./C4%20model.md). The C4 diagram shows deployable units and how they communicate. A context map shows model boundaries and team relationships, and one context may span several deployed services. Update it when integrations change.

_Usage:_

"Who consumes the `CustomerUpdated` event?"

"Nobody knows, which is why the last rename broke fulfilment. Let's draw a context map before changing it."
