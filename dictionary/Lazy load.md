---
description: Deferring the loading of related data until code first accesses it, at the risk of hidden N+1 queries.
---

Lazy load is a pattern in which an object defers loading related data until code first accesses it. A `Customer` can be fetched without its orders, and the orders are queried only when something asks for them. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002), and most ORMs offer it as an option or a default.

```typescript
class Customer {
  private orders?: Order[];

  constructor(
    readonly id: string,
    private loadOrders: (id: string) => Promise<Order[]>,
  ) {}

  async getOrders() {
    this.orders ??= await this.loadOrders(this.id);
    return this.orders;
  }
}
```

The pattern avoids loading data that a use case never reads. Fetching a customer to show a name should not pull thousands of order rows. Fowler describes four forms:

| Form                | How it works                                                  |
| ------------------- | ------------------------------------------------------------- |
| Lazy initialisation | A field starts empty and is loaded on first access            |
| Virtual proxy       | A [proxy](./Proxy%20pattern.md) stands in and loads when used |
| Value holder        | A wrapper object loads the value when asked                   |
| Ghost               | A partial object loads its remaining fields on first access   |

The best-known failure is the N+1 query problem. A list page loads 50 orders, then a template reads `order.customer.name` for each one, issuing one query per row. The page is quick in development with five rows and slow in production, and nothing in the template looks like a database call. This makes lazy loading a [leaky abstraction](./Leaky%20abstraction.md), because a property access can carry a network round trip.

A related failure occurs after the session closes. In Hibernate, touching an unloaded relation outside its session throws `LazyInitializationException`, often in a view or serialiser far from the original query.

To use it safely, fetch what a use case needs up front with a join or batch query, and keep laziness for data that is rarely read. Log query counts per request in development so N+1 patterns appear before release. Lazy load differs from pagination and caching: it changes when data is fetched, while pagination limits how much is fetched and caching avoids fetching it again.

_Usage:_

"The orders page makes 340 queries."

"Each row lazily loads its customer. Fetch the customers in one batch with the list query."
