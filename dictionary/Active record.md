---
description: An object that wraps a database row and carries both its domain logic and its own persistence methods.
---

Active record is a pattern in which an object wraps one database row, holding the row's columns as fields along with the domain logic and the methods that load and save it. A `User` instance has an `email` property, a `confirm()` method and a `save()` method. Martin Fowler named the pattern in Patterns of Enterprise Application Architecture (2002), and Ruby on Rails adopted the name for its ORM.

```typescript
class User extends Model {
  email!: string;
  confirmedAt: Date | null = null;

  confirm() {
    this.confirmedAt = new Date();
    return this.save();
  }
}

const user = await User.findById(id);
await user.confirm();
```

The pattern suits applications whose objects map closely to tables. It needs little code, new developers can follow it quickly, and frameworks such as Rails and Laravel's Eloquent provide queries, validations and migrations around it. For many CRUD products it is a productive default.

The trade-offs appear as the domain diverges from the schema. Because persistence is part of the object, business logic is hard to test without a database or a stubbed framework. Lifecycle callbacks add hidden behaviour: a script that updates one column sends a welcome email because an `afterSave` hook fired. Models also tend to grow into [god objects](./God%20object.md), since every feature that touches users adds methods to `User`.

| Concern               | Active record             | [Data mapper](./Data%20mapper.md)       |
| --------------------- | ------------------------- | --------------------------------------- |
| Who saves the object  | The object itself         | A separate mapper                       |
| Object shape          | Mirrors the table         | Can differ from the table               |
| Testing domain logic  | Usually needs a database  | Plain objects                           |
| Setup cost            | Low                       | Higher                                  |
| Fits                  | Schema-shaped domains     | A complex [domain model](./Domain%20model.md) |

To contain the costs, reserve callbacks for data integrity, move workflows that span models into a [service layer](./Service%20layer.md), and extract complicated rules into plain objects. Migrating from active record to a data mapper later is expensive, because calling code across the application depends on the persistence methods. Base the choice on how far the domain is likely to diverge from its tables.

_Usage:_

"Why did the backfill email every customer?"

"`User` has an `afterSave` hook that sends the notification. Run the backfill with callbacks skipped, then move that email into the signup use case."
