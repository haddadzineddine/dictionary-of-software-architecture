---
description: Reusing a fixed set of expensive objects by borrowing and returning them instead of creating and destroying each one.
---

An object pool keeps a set of initialised objects ready for reuse. Code borrows an object, uses it and returns it, so the program avoids repeating expensive creation and destruction. The pattern is not one of the 23 in the Gang of Four book. Database connection pools and thread pools are its common forms.

```typescript
class Pool<T> {
  private waiting: ((item: T) => void)[] = [];

  constructor(private idle: T[]) {}

  acquire(): Promise<T> {
    const item = this.idle.pop();
    if (item !== undefined) return Promise.resolve(item);
    return new Promise((resolve) => this.waiting.push(resolve));
  }

  release(item: T) {
    const next = this.waiting.shift();
    if (next) next(item);
    else this.idle.push(item);
  }
}
```

A pool suits objects that are costly to create, such as a database connection that needs a network handshake and authentication. It also caps usage: a pool of 20 connections stops a traffic spike from opening thousands against the database.

One common failure is pool exhaustion. If a code path throws before releasing a connection, that connection is lost to the pool. After enough errors, requests hang waiting for a connection while the database looks idle. Release in a `finally` block or use a helper that manages the lifetime, and set an acquire timeout so callers fail with a clear error.

```typescript
const conn = await pool.acquire();
try {
  return await conn.query(sql);
} finally {
  pool.release(conn);
}
```

The second failure is leftover state. A reused connection can still carry a session variable or an open transaction from its previous borrower, which then affects an unrelated request. Reset each object on return, and discard any that are broken rather than returning them.

Holding a connection while making a slow external call is a related mistake, because it ties up a scarce resource during work that does not need it.

Do not pool cheap objects. In garbage-collected runtimes, allocating small objects is inexpensive, and a hand-written pool adds state bugs for little gain, so measure first. A pool differs from a [flyweight](./Flyweight%20pattern.md): a pooled object is used exclusively by one borrower at a time, while a flyweight is shared by many users at once and must be immutable.

_Usage:_

"The API is hanging, but the database is nearly idle."

"Check the pool. The error path in checkout never releases its connection, so we've run out."
