---
description: Restructuring teams deliberately so their communication paths produce the software architecture you want.
---

The inverse Conway maneuver is the practice of restructuring teams so that their communication paths produce a desired software design. It applies [Conway's law](./Conway's%20law.md) in reverse: instead of letting the organisation determine the design, leaders choose the design and shape the organisation to match.

It addresses architecture plans that fail against the existing org chart. A company draws independent services on a whiteboard, but one shared database team must approve every schema change and one frontend team integrates every feature. The services deploy separately in name only, and the result is a [distributed monolith](./Distributed%20monolith.md).

| Step                   | Who                           | What happens                                               |
| ---------------------- | ----------------------------- | ---------------------------------------------------------- |
| 1. Define the target   | Architects, engineering leads | Identify boundaries that should change independently       |
| 2. Map the gap         | Engineering leads             | Compare current team communication with those boundaries   |
| 3. Redraw teams        | Leadership                    | Give each team end-to-end ownership of one boundary        |
| 4. Move ownership      | Teams                         | Transfer code, data and on-call responsibility             |
| 5. Reduce coordination | Teams                         | Replace shared approvals with contracts and self-service tools |
| 6. Review              | Engineering leads             | Check whether changes now stay within one team             |

[Team Topologies](./Team%20Topologies.md) provides team types and interaction modes for step 3.

The main risk is choosing the wrong boundary. Once a team owns a boundary, people, roadmaps and code all reinforce it, so a mistaken split becomes expensive to change. Validate a boundary first by examining which code changes together and by trying it in one area of the business. A [context map](./Context%20map.md) can help identify candidates.

A reorganisation also has costs: lost working relationships, interrupted delivery and displaced knowledge. Do not use the maneuver on a small codebase, or where the current structure causes no coordination problems. Moving people without the matching technical work achieves little, because the old code keeps forcing teams to coordinate, so move ownership and code together.

_Usage:_

"We split into services, but every release still needs the DBA team's approval."

"The team structure didn't change. Give each domain team ownership of its schema and deployments."
