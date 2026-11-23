---
description: The part of a business that differentiates it from competitors and deserves the most design investment.
---

A core domain is the part of a business that differentiates it from competitors and that it must do well to succeed. For a logistics company it might be route optimisation, and for an insurer it might be risk pricing. Eric Evans defined the term as part of strategic design in Domain-Driven Design (2003). It is one of three types of [subdomain](./Subdomain.md), alongside supporting and generic.

Identifying a core domain directs limited engineering effort. Without that decision, effort tends to follow technical interest: senior engineers build an in-house authentication system or workflow engine, while the pricing rules that win customers stay in an unowned script that nobody wants to change. The result is polished code in areas a vendor could have supplied and fragile code in the area that decides revenue.

The term is easily confused with "important". Payroll is essential and a failure would be serious, but it rarely distinguishes one company from another, so it is usually generic and bought. The test is whether doing it better than competitors would win business.

| Question                                    | If yes                        | If no                          |
| ------------------------------------------- | ----------------------------- | ------------------------------ |
| Would doing this better win customers?      | Candidate for a core domain   | Supporting or generic          |
| Could a vendor supply it equally well?      | Buy it                        | Consider building it           |
| Do its rules change with business strategy? | Keep in-house, model carefully | A simple implementation may do |

A core domain justifies investment that other areas do not: a rich [domain model](./Domain%20model.md), close work with domain experts, a precise [ubiquitous language](./Ubiquitous%20language.md) and experienced engineers. Protect it from vendor and legacy models with an [anti-corruption layer](./Anti-corruption%20layer.md), so that outside concepts do not shape its design.

Keep the list short, since a company that labels everything as core has made no decision. The classification can also change. A capability that once set a company apart may become a commodity, at which point it should be simplified or replaced with a product.

_Usage:_

"Should we spend next quarter rebuilding the notification service?"

"Notifications are generic for us. Use a vendor and put that time into the pricing engine, which is our core domain."
