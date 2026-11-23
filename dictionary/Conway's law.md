---
description: The observation that organisations design systems whose structure mirrors their own communication structure.
---

Conway's law states that an organisation designing a system will produce a design whose structure mirrors the organisation's communication structure. Melvin Conway published the observation in 1968 in the article "How Do Committees Invent?".

The mechanism is communication cost. Engineers on one team can adjust a shared interface in a conversation, so code within a team tends to be tightly integrated. Across teams, changes require meetings and agreements, so teams settle on narrow interfaces at their boundary. Over time, module boundaries settle where the team boundaries are.

The effect is visible when a simple feature needs changes from three teams and waits in three backlogs, because the system was divided along the org chart rather than along the problem. A website whose navigation follows company departments instead of user tasks is another example.

| Organisation                                 | Likely architecture                      |
| -------------------------------------------- | ---------------------------------------- |
| Separate frontend, backend and database teams | Layers with handoffs at each boundary    |
| One team per business capability             | Services aligned with capabilities       |
| A single team across the product             | A monolith with fluid internal boundaries |
| Outsourced vendor for one subsystem          | A formal, rigid interface at the contract line |

Conway's law describes a tendency rather than a strict rule. Deliberate interfaces and technical leadership can work against it, but a design that conflicts with how teams communicate needs continuous effort to maintain. A [distributed monolith](./Distributed%20monolith.md) often appears when a system is split into services while the same people and approvals still coordinate every release.

Treat the org chart as an architectural input. Before approving a target design, check whether teams can own its parts with little coordination. If they cannot, change the design or the teams. Changing teams deliberately to obtain a design is the [inverse Conway maneuver](./Inverse%20Conway%20maneuver.md), and [Team Topologies](./Team%20Topologies.md) offers a vocabulary for that work.

_Usage:_

"Why does adding a shipping option need the web, orders and logistics teams?"

"The system is split the way we're organised. That's Conway's law."
