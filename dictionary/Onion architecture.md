---
description: Arranging code in rings around a domain model, with infrastructure on the outside and dependencies pointing inward.
---

Onion architecture arranges an application in concentric rings around its [domain model](./Domain%20model.md), with every dependency pointing toward the centre. Jeffrey Palermo named it in 2008 as an alternative to layered architecture, in which business code sits above and depends on the data access layer.

That dependency causes a recognisable problem. Replacing the ORM or changing a table forces edits to business classes, because those classes import data access types. A unit test for a pricing rule then needs a database.

| Ring                                     | Contains                                                                        | May depend on   |
| ---------------------------------------- | ------------------------------------------------------------------------------- | --------------- |
| Domain model                             | [Entities](./Entity.md), [value objects](./Value%20object.md), business rules   | Nothing         |
| [Domain services](./Domain%20service.md) | Logic spanning several objects, repository interfaces                           | Domain model    |
| Application services                     | Use cases, transaction boundaries                                               | Both inner rings |
| Infrastructure and UI                    | Database code, HTTP, messaging, tests                                           | All inner rings |

The inner rings declare what they need as interfaces. The outer ring implements them and connects them at startup, usually through dependency injection.

```typescript
// Domain services ring
interface CustomerRepository {
  findById(id: CustomerId): Promise<Customer | null>;
}

// Infrastructure ring
class SqlCustomerRepository implements CustomerRepository {
  async findById(id: CustomerId) {
    /* query and map to a Customer */
    return null;
  }
}
```

The cost is indirection and mapping. Each external shape must be translated at the boundary, and a simple read may pass through several types that add nothing. Onion architecture suits long-lived systems with substantial business rules. For a small CRUD service, a [transaction script](./Transaction%20script.md) with direct queries is easier to maintain.

Onion architecture is most often confused with [clean architecture](./Clean%20architecture.md). Both enforce inward dependencies and keep frameworks at the edge. Onion places the domain model at the centre and emphasises where repository interfaces live, while clean architecture names an explicit use case ring and a ring of interface adapters. A team following either will produce similar code, so pick one vocabulary and use it consistently.

_Usage:_

"Why does the pricing class import our ORM's decorators?"

"It shouldn't. Move the mapping to infrastructure and keep a plain domain class in the centre."
