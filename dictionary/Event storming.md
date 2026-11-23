---
description: A workshop where developers and domain experts map a business process as a timeline of events on sticky notes.
---

Event storming is a collaborative workshop in which developers and domain experts map a business process as a timeline of [domain events](./Domain%20event.md) on sticky notes. Alberto Brandolini created the technique. Participants work on a long wall or shared digital board, writing past-tense statements such as "Order placed" and "Payment failed".

The workshop addresses knowledge that is spread across people. Requirements documents often describe the intended process, each department knows only its own step, and contradictions surface after code is written. In a workshop, a warehouse lead can point out that "order shipped" happens twice for split deliveries, which nobody in engineering knew. Finding that on a wall takes minutes, while finding it in production can mean a data migration.

| Step                | Who         | What happens                                                                |
| ------------------- | ----------- | --------------------------------------------------------------------------- |
| Explore             | Everyone    | Write events on orange notes, without ordering them                         |
| Timeline            | Everyone    | Arrange events in order and merge duplicates                                |
| Hotspots            | Facilitator | Mark disagreements and unknowns in a contrasting colour                     |
| Commands and actors | Group       | Add what triggered each event and who did it                                |
| Policies            | Group       | Add rules of the form "whenever X happens, do Y"                            |
| Boundaries          | Group       | Group related events into candidate contexts and [aggregates](./Aggregate.md) |

Brandolini describes formats at different levels of detail. A Big Picture session covers an entire business and looks for problems and opportunities. Process Modelling examines one process. Software Design goes further, towards aggregates and code.

Results depend on who attends. Without the people who do the work, the group documents its own assumptions and the session adds little. A facilitator keeps the discussion moving and records disputes as hotspots, so the group does not stop to resolve each one.

The output is a shared understanding plus inputs to design: a draft [ubiquitous language](./Ubiquitous%20language.md), candidate boundaries for a [context map](./Context%20map.md) and a list of open questions. It is not a finished design, and the wall should not be transcribed one to one into classes. For a small, well-understood feature, a conversation is enough.

_Usage:_

"Sales, ops and finance each describe refunds differently."

"Let's run an event storming session with all three and mark the disagreements as hotspots."
