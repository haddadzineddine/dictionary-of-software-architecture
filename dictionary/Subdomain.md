---
description: A distinct area of a business's activity, classified as core, supporting or generic to guide investment.
---

A subdomain is a distinct area of a business's overall activity, such as pricing, billing, shipping or identity. The term comes from Eric Evans's Domain-Driven Design (2003), and it describes the business itself and not the software. An online retailer has these areas whether it runs one application or fifty.

Subdomains are usually classified into three types:

| Type                          | Description                                     | Typical approach             | Retailer example  |
| ----------------------------- | ----------------------------------------------- | ---------------------------- | ----------------- |
| [Core](./Core%20domain.md)    | Differentiates the business                     | Build in-house, model richly | Pricing           |
| Supporting                    | Specific to the business but not differentiating | Build simply or outsource   | Returns handling  |
| Generic                       | The same problem in most businesses             | Buy or use open source       | Payments, email   |

The classification guides where to spend engineering effort. Without it, teams apply the same level of design everywhere, so an internal admin screen receives an elaborate model while the rules that earn revenue sit in an untested script. Classifying subdomains makes that imbalance visible and supports decisions about what to build, buy or keep simple. A generic subdomain is often best served by a vendor behind a [gateway](./Gateway%20pattern.md).

The type depends on the business. Payments is generic for a bookshop and a core domain for a payments company. Classification also changes over time, as a capability that once differentiated a company becomes a commodity available from vendors.

A subdomain differs from a bounded context. The subdomain belongs to the problem space and describes what the business does. A bounded context belongs to the solution space and marks a boundary within which one model and its [ubiquitous language](./Ubiquitous%20language.md) apply. Aligning them one to one is a reasonable starting point, but legacy systems often have one context covering several subdomains, and a large subdomain may be split across contexts.

Identify subdomains by asking domain experts what the business does and where the work differs. The existing module structure is a weak guide, because it may reflect history or team layout, as [Conway's law](./Conway's%20law.md) predicts.

_Usage:_

"Should we write our own invoicing engine?"

"Invoicing is a generic subdomain for us. Buy one and keep our engineers on pricing."
