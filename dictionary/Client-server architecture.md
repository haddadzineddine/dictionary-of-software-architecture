---
description: Dividing a system into clients that initiate requests and servers that provide shared data or services in response.
---

Client-server architecture divides a system into clients, which initiate requests, and servers, which respond with data or perform work. A browser loading a page, a mobile app calling an API and an application connecting to a database are all client-server relationships. One program can play both roles: an API server is a server to its callers and a client of its database.

Centralising shared state and rules on the server makes them easier to update, secure and back up. Clients can be numerous and varied, because they only need to speak the protocol.

The split determines what each side can be trusted with. The server must treat all client input as untrusted, because a user can modify the client or call the API directly. A common failure is a discount or permission check performed only in the browser, which someone bypasses by replaying an edited request. Validate on the client for responsiveness and on the server for correctness.

| Variant        | Client does              | Server does             | Trade-off                               |
| -------------- | ------------------------ | ----------------------- | --------------------------------------- |
| Thin client    | Displays output          | Rendering and logic     | Simple to update, needs network         |
| Rich client    | UI logic and local state | Data and business rules | Responsive, more duplicated logic       |
| Offline client | Works on a local copy    | Synchronises changes    | Usable offline, needs conflict handling |

Clients and servers also change at different speeds. A web server deploys in minutes, while older mobile app versions may keep calling the API for years. Removing a response field can crash those versions even though all server tests pass, so API changes need to stay backward compatible or be versioned.

The server can become a bottleneck or single point of failure, which replication and load balancing address. [Peer-to-peer architecture](./Peer-to-peer%20architecture.md) removes the central role, at the cost of harder coordination and trust. Most product systems remain client-server because a central authority simplifies consistency, access control and operations.

_Usage:_

"Someone got a 100% discount by editing the checkout request."

"The limit is only enforced in the frontend. The server has to validate it too."
