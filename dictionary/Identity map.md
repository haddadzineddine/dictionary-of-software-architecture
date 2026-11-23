---
description: A per-session registry that ensures each database row is loaded into exactly one in-memory object.
---

An identity map is a registry that records every object loaded during a session, keyed by its database identity, so the same row always resolves to the same in-memory object. Before loading a row, the data access code checks the map and returns the existing instance if there is one. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002).

```typescript
class IdentityMap<T> {
  private items = new Map<string, T>();

  get(id: string) {
    return this.items.get(id);
  }

  add(id: string, item: T) {
    this.items.set(id, item);
  }
}

async function findUser(map: IdentityMap<User>, mapper: UserMapper, id: string) {
  const known = map.get(id);
  if (known) return known;

  const user = await mapper.load(id);
  map.add(id, user);
  return user;
}
```

The pattern prevents two copies of one row from diverging within a single request. Without it, one function loads customer 42 and changes the email, another loads customer 42 and changes the plan, and whichever saves last overwrites the other's change. The result is a lost update with no error. With a map, both functions hold the same object, and both changes are saved.

An identity map usually lives inside a [unit of work](./Unit%20of%20work.md), and [data mapper](./Data%20mapper.md) libraries such as Hibernate and SQLAlchemy provide one in their sessions. It should last only as long as that session. A process-wide map keeps objects alive indefinitely, serves stale data, and can expose one user's data to another request.

The main surprise is stale reads within a session. If a raw SQL statement or another process updates a row, loading it again through the session may return the object with its old field values, because the existing instance takes precedence. The fix is an explicit refresh, or ending the session before re-reading.

An identity map differs from a cache. A cache exists to avoid work, may be shared across requests and needs an expiry policy. An identity map exists to guarantee one object per row inside a session. It can save a query when loading by primary key, but a query on other criteria still goes to the database and then resolves the returned rows to existing instances.

_Usage:_

"The test updates the row with raw SQL, but `findById` still returns the old status."

"The session's identity map is handing back the loaded instance. Refresh it or read through a new session."
