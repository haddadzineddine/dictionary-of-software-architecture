---
description: Splitting a system into isolated full copies of its stack, each serving a subset of customers to limit failure impact.
---

Cell-based architecture splits a system into multiple isolated units, called cells, each running a complete copy of the stack and serving a subset of customers. A thin routing layer sends each request to the customer's cell. Cells share as little as possible, including data stores.

The style limits blast radius, the share of customers affected by a failure. In a single shared deployment, one tenant's runaway query, a poison message or a bad configuration push can take down the service for everyone. With twenty equally sized cells, the same fault is normally contained to one cell, or five percent of customers.

| Part          | Role                                                       |
| ------------- | ---------------------------------------------------------- |
| Cell          | Independent full stack with its own compute and data       |
| Partition key | Value, often a tenant ID, that assigns a request to a cell |
| Cell router   | Maps a key to a cell and forwards the request              |
| Control plane | Creates cells, assigns tenants and moves them between cells |

Deployments roll out one cell at a time, so a faulty release can be caught before it reaches the whole fleet. Capacity grows by adding cells, and each cell has a known maximum size that can be load tested.

The router is shared by every request, so it must remain simple and highly available. Business logic placed there recreates the shared failure domain that cells were meant to remove. Other costs include running many copies of the infrastructure, moving tenants between cells, and building a separate path for cross-cell features such as global search or organisation-wide reports. Small systems rarely justify this overhead.

Cell-based architecture differs from two nearby techniques. Database sharding partitions only data, so a fault in a shared application tier still affects all shards. A bulkhead isolates resources inside a service, such as separate connection pools, whereas a cell isolates the entire stack.

_Usage:_

"One customer's bulk import took the API down for everyone again."

"If we move to cells, that import only affects the customers in its cell."
