---
description: A reusable template of components, patterns and decisions for building a class of systems in a given context.
---

A reference architecture is a reusable template describing the components, patterns, technology choices and decisions for a class of systems. An organisation might publish one for customer-facing web services, and cloud vendors publish them for workloads such as data lakes and web applications.

It addresses teams solving the same problems differently. Without a shared starting point, each new service invents its own logging, authentication and deployment, so on-call engineers must relearn every system and security reviews start from zero. A reference architecture gives teams a default that has already been reviewed.

| Artefact               | Scope                        | Example                             |
| ---------------------- | ---------------------------- | ----------------------------------- |
| Design pattern         | One recurring design problem | [Strategy pattern](./Strategy%20pattern.md) |
| Reference architecture | A class of systems           | Standard event-processing service   |
| Solution architecture  | One specific system          | The design of our payments service  |
| Service template       | Executable starting point    | A scaffold implementing the reference |

A useful reference architecture states what it is for, which [quality attributes](./Quality%20attribute.md) it targets, when it does not apply and why each major choice was made. Pair the document with a working example or scaffold, because teams follow code more reliably than diagrams.

The common failure is applying it regardless of fit. A small internal tool inherits a queue, three clusters and a service mesh because the template requires them, and then costs more to run than it delivers. This is a form of [golden hammer](./Golden%20hammer.md). Allow exceptions, and ask teams to explain them in an [architecture decision record](./Architecture%20decision%20record.md). Frequent exceptions indicate that the reference needs revising.

Reference architectures also age. One written for a past technology stack keeps steering new work toward it unless it has an owner and a review schedule. Vendor reference architectures are designed around that vendor's products, so treat them as input rather than instruction.

_Usage:_

"Do we need the full event pipeline for this little admin tool?"

"No. The reference covers high-volume services. Record the exception and build a simple CRUD app."
