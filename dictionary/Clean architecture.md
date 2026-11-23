---
description: Organising code in concentric rings so business rules depend on nothing, and frameworks and databases depend on them.
---

Clean architecture organises a system into concentric rings in which source code dependencies point only inward. Robert C. Martin set it out in his 2017 book _Clean Architecture_. The inward-only constraint is called the dependency rule: an inner ring never names anything from an outer ring.

| Ring                   | Contains                                  | Example                                 |
| ---------------------- | ----------------------------------------- | --------------------------------------- |
| [Entities](./Entity.md) | Enterprise-wide business rules            | `Invoice`                               |
| Use cases              | Application-specific workflows            | `ApproveInvoice`                        |
| Interface adapters     | Translation to and from external formats  | Controllers, presenters, store classes  |
| Frameworks and drivers | External tools                            | Web framework, ORM, database            |

It addresses business logic that cannot be tested or moved because it is entangled with a framework. A framework upgrade breaks pricing code, or a test of one discount calculation needs a running database. Under the dependency rule, the use case declares an interface and an outer ring implements it, which applies the [dependency inversion principle](./Dependency%20inversion%20principle.md).

```typescript
// Use case ring: owns the interface
interface InvoiceStore {
  find(id: string): Promise<Invoice>;
  save(invoice: Invoice): Promise<void>;
}

class ApproveInvoice {
  constructor(private readonly invoices: InvoiceStore) {}

  async run(id: string): Promise<void> {
    const invoice = await this.invoices.find(id);
    invoice.approve();
    await this.invoices.save(invoice);
  }
}

// Adapter ring: depends inward
class PostgresInvoiceStore implements InvoiceStore {
  /* SQL here */
}
```

The structure has a cost. Adding one field to a screen can require changes to an entity, a use case's input and output models, a presenter and a mapper. For a CRUD application with little logic, those layers add translation without protecting anything, and a [transaction script](./Transaction%20script.md) or [vertical slice architecture](./Vertical%20slice%20architecture.md) fits better. Apply the rings where business rules are complex and expected to outlive their delivery mechanism.

Clean architecture is often confused with hexagonal architecture and [onion architecture](./Onion%20architecture.md). All three keep domain code independent of infrastructure. Hexagonal architecture describes ports and adapters without prescribing inner layers, while onion and clean architecture name rings inside the application. The resulting code is often similar.

_Usage:_

"Testing the discount rule needs Postgres and a running web server."

"The rule is in the controller. Move it into a use case and give it a store interface."
