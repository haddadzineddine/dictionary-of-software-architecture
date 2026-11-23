---
description: Scaling by processing requests against replicated in-memory data grids, with the database updated asynchronously.
---

Space-based architecture removes the database from the synchronous request path by processing transactions against replicated in-memory data. Application instances, called processing units, each hold the data they need, and changes are written to the database asynchronously. The name comes from the tuple space, a shared associative memory.

It addresses load that the database cannot absorb. During a ticket sale, web servers can be added in seconds, but requests still queue on a saturated database connection pool and the site times out. With the working data in memory, adding processing units adds both compute and data capacity.

| Component              | Role                                                     |
| ---------------------- | -------------------------------------------------------- |
| Processing unit        | Runs application code with an in-memory copy of its data |
| Data grid              | Replicates changes between processing units              |
| Messaging grid         | Routes incoming requests to available units              |
| Processing grid        | Coordinates requests that span several unit types        |
| Deployment manager     | Starts and stops units as load changes                   |
| Data pump              | Sends updates toward the database asynchronously         |
| Data writer and reader | Persist updates, and reload data after a restart         |

The trade-offs follow from asynchronous persistence. Updates accepted in memory can be lost if units fail before the pump delivers them. Two units can sell the same seat when replication lags, so conflicts need a resolution rule. Memory is costly, and realistic failure testing needs production-like load.

Use the style for spiky, high-volume workloads such as ticketing and auctions, where brief inconsistency can be reconciled. Avoid it for workloads that must enforce strict [invariants](./Invariant.md) at commit, such as a ledger, for datasets too large to hold in memory, and for steady, moderate load.

Space-based architecture is often confused with adding a cache. A cache sits beside a database that remains the primary store for transactions, and writes normally still reach that database synchronously. In space-based architecture the grid is the working store for transactions, and the database is a durable copy that lags behind.

_Usage:_

"During on-sale the app servers idle while the database pool is exhausted."

"Caching reads won't fix the writes. We could hold seat inventory in a data grid and persist asynchronously."
