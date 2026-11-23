---
description: A layer that moves data between objects and a database while keeping each unaware of the other.
---

A data mapper is a layer that moves data between in-memory objects and a database while keeping the two independent of each other. The domain objects contain no SQL and do not know a database exists, and the schema does not need to match the object structure. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002). Hibernate, SQLAlchemy's ORM and Doctrine are widely used implementations.

```typescript
class OrderMapper {
  constructor(private db: Db) {}

  async findById(id: string): Promise<Order | null> {
    const row = await this.db.one("select * from orders where id = $1", [id]);
    return row ? new Order(row.id, Money.cents(row.total_cents), row.status) : null;
  }

  async update(order: Order) {
    await this.db.none("update orders set status = $1 where id = $2", [
      order.status,
      order.id,
    ]);
  }
}
```

The pattern addresses the mismatch between object and relational structure. A `Customer` may hold an `Address` [value object](./Value%20object.md) and a list of preferences, while the database stores them across three tables with legacy column names. With [active record](./Active%20record.md), the object has to mirror those tables, so a schema change reaches business code. With a mapper, only the mapping changes, and the [domain model](./Domain%20model.md) can be tested without a database. Teams often notice the need when a column rename touches dozens of business files, or when a unit test for a pricing rule requires a running Postgres instance.

The costs are extra code and indirection. Each field is named in the object, the mapping and the schema, so a new column needs changes in all three. Mapping libraries remove some of this work but add configuration and behaviour of their own. For tables that map one to one onto simple objects, a mapper has little to separate, and active record is usually simpler.

Mapping libraries commonly combine a data mapper with a [unit of work](./Unit%20of%20work.md) to batch writes and an [identity map](./Identity%20map.md) to avoid duplicate instances of a row.

A data mapper is often confused with the repository pattern. The mapper deals in rows and fields and knows the schema. A repository sits above it, exposing a collection-like interface in domain terms such as `findOverdue()`, and uses a mapper for the translation. In small codebases, one class may perform both roles.

_Usage:_

"Renaming `cust_ref` touched thirty files."

"Those files read row fields directly. Put a data mapper in front of the table so the next rename lives in one place."
