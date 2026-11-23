---
description: Connecting nodes that act as both client and server, sharing work and data directly without relying on a central server.
---

Peer-to-peer (P2P) architecture connects nodes, called peers, that act as both client and server. Peers exchange data or work with each other rather than relying on a central server. Examples include BitTorrent for file distribution, Bitcoin for a shared ledger and WebRTC data channels for direct browser connections.

Capacity can grow with participation, because each peer that downloads a file can also upload it to others. No single server failure stops the network, and the operator's bandwidth costs can fall. In exchange, the system must solve problems that a central server handles implicitly: finding peers, agreeing on state and deciding whom to trust.

| Topology     | How peers are found                   | Trade-off                                     |
| ------------ | ------------------------------------- | --------------------------------------------- |
| Unstructured | Flooding or gossip between neighbours | Simple and resilient, lookups are inefficient |
| Structured   | Distributed hash table                | Efficient lookups, more upkeep during churn   |
| Hybrid       | Central tracker or signalling server  | Easy discovery, retains a central dependency  |

Network conditions are the first practical obstacle. A P2P feature often works between two machines on the same network and then fails between real users, because NAT on home routers and corporate firewalls blocks inbound connections. Applications use techniques such as STUN and hole punching, and fall back to a TURN relay when no direct path exists.

Peers also join and leave constantly, which is known as churn, so data must be replicated and no peer can be assumed to stay online. Peers cannot be trusted by default either. They may send corrupted data or create many fake identities to gain influence, which is called a Sybil attack. Content hashes, signatures and consensus protocols limit this.

Choose P2P when decentralisation, censorship resistance or distribution cost justifies the complexity. For most applications, [client-server architecture](./Client-server%20architecture.md) is simpler to secure, monitor and update, because it has one authority to operate.

_Usage:_

"Video calls work in the office but fail for half our customers."

"They're behind NAT. We need a TURN relay for when direct connections can't be established."
