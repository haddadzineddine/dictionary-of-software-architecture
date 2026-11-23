---
description: An object that tracks changes during a business operation and writes them to the database as one commit.
---

A unit of work is an object that tracks the changes made during a business operation and writes them to the database together, as one commit. Code loads and modifies objects in memory, and the unit of work determines which inserts, updates and deletes are needed. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002). Hibernate's `Session`, Entity Framework's `DbContext` and SQLAlchemy's `Session` are implementations.

```typescript
async function payOrder(uow: UnitOfWork, orderId: OrderId, payment: Payment) {
  const order = await uow.orders.get(orderId);
  order.markPaid(payment);
  uow.ledger.add(LedgerEntry.forPayment(order, payment));
  await uow.commit();
}
```

The pattern prevents operations that half-succeed. If `orders.save()` and `ledger.save()` each commit on their own, a crash between them leaves an order marked as paid with no ledger entry, and the data stays wrong until a reconciliation finds it. With a unit of work, both changes commit or neither does.

| Step    | Who                                    | What happens                                     |
| ------- | -------------------------------------- | ------------------------------------------------ |
| Begin   | [Service layer](./Service%20layer.md)  | Opens a unit of work for the use case            |
| Load    | Repositories or mappers                | Read objects and register them as tracked        |
| Change  | Domain objects                         | Modify state in memory                           |
| Commit  | Unit of work                           | Computes the changes, writes in one transaction  |
| Failure | Unit of work                           | Rolls back and discards tracked state            |

Deferring writes until commit causes some surprises. A query issued mid-operation may not see pending changes unless the library flushes first, and constraint violations appear at commit, far from the line that caused them. A unit of work also cannot cover external effects. An email sent before commit still goes out if the commit fails, so send it afterwards or record it with the outbox pattern.

A unit of work differs from a database transaction. The transaction is the storage guarantee, while the unit of work is the application-level object that collects changes and applies them in one at commit. Keep it scoped to one request or job, because a long-lived one accumulates tracked objects and stale state. It often uses an [identity map](./Identity%20map.md) so that each row is tracked once.

For a single-table update, a plain database transaction is enough.

_Usage:_

"We have paid orders with no ledger entries."

"Each repository commits separately. Wrap the payment in one unit of work so both writes succeed or fail together."
