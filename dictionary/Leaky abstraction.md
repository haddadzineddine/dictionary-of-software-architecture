---
description: An abstraction whose hidden details show through, forcing its users to understand the layer it was meant to hide.
---

A leaky [abstraction](./Abstraction.md) is one whose hidden details affect the people using it, so they have to understand the layer underneath anyway. Joel Spolsky popularised the term in his 2002 essay "The Law of Leaky Abstractions", which argued that all non-trivial abstractions leak to some degree.

The symptom is code that works until it meets a condition the interface did not mention. An ORM using [lazy loading](./Lazy%20load.md) makes a list page look like ordinary object access, then the page takes eight seconds because each `order.customer` runs a query. A remote call looks like a local function until the network times out.

| Abstraction           | What it hides        | How it leaks                         |
| --------------------- | -------------------- | ------------------------------------ |
| ORM                   | SQL and query plans  | N+1 queries, missing indexes         |
| Remote procedure call | The network          | Timeouts, partial failure, retries   |
| Filesystem            | Disks and mounts     | Slow or failed writes on network drives |
| Garbage collection    | Memory management    | Pauses, leaks through held references |
| `async`/`await`       | Concurrency          | Interleaving between awaits          |
| Object storage folders | A flat key space    | A rename is a copy and a delete      |

Some leaks come from design choices and can be avoided. A data access method that returns a query builder, a service that throws `PrismaClientKnownRequestError`, or a domain type with a `_id` field passes an implementation detail to callers. Return domain types, translate errors at the boundary, and use an [adapter](./Adapter%20pattern.md) or [anti-corruption layer](./Anti-corruption%20layer.md) around external systems.

Other leaks cannot be removed, because latency, failure and resource limits come from the hardware and network. For those, make the cost visible in the interface: return a `Promise`, accept a timeout, and offer batch operations. Presenting a network call as a plain getter hides information callers need.

Teams should know one level below the abstractions they rely on, such as SQL for ORM users and TCP basics for anyone calling HTTP services. The abstraction saves time in normal operation, and that knowledge is needed when it fails.

_Usage:_

"The orders page got slow, but the code is just a loop over `order.customer`."

"That property runs a query each time. The ORM is leaking, so load customers in one batch."
