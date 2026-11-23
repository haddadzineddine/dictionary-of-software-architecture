---
description: A design guideline to prefer the simplest solution that meets the requirement, because complexity has a lasting cost.
---

KISS stands for "keep it simple, stupid", a guideline to choose the simplest design that meets the requirement. The phrase is commonly attributed to Lockheed engineer Kelly Johnson. In software, it means avoiding moving parts the problem does not require.

The symptom is a small task that takes days because of the structure around it. Adding a field to a form means editing a controller, a service, a mapper, two [data transfer objects](./Data%20transfer%20object.md) and a factory, each of which only forwards the value. New team members need a diagram to follow a single request, and bugs appear in the handoffs between layers.

Complexity has a running cost. Everyone who reads, debugs or changes the code pays it, long after the person who added it has moved on. Simple code is easier to test, delete and replace.

Simple does not mean short. A clever one-liner can be harder to follow than five plain lines, and a single large script can be harder to maintain than two well-named modules. A useful test is how much a reader must hold in their head to make a correct change.

| Choice     | Simpler default         | Reach for more when                  |
| ---------- | ----------------------- | ------------------------------------ |
| Storage    | One relational database | A measured load or data shape needs it |
| Deployment | A single deployable     | Team or scaling needs diverge        |
| Variation  | An `if` statement       | Several variants keep growing        |
| Reuse      | A plain function        | Several callers share real knowledge |

KISS can be misused to reject necessary work. Error handling, input validation and security are required complexity, and removing them makes a system shorter but not simpler. Distinguish essential complexity, which comes from the problem, from accidental complexity, which comes from the solution. KISS targets the second. It is closely related to [YAGNI](./YAGNI.md), which is about not building for imagined future needs, whereas KISS concerns the shape of what you do build.

_Usage:_

"Do we need a queue and a worker for this nightly export?"

"It runs once a day and takes a minute. A cron job calling one function is enough."
