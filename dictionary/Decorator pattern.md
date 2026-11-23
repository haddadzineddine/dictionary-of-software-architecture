---
description: Wrapping an object with another that has the same interface to add behaviour without changing the original class.
---

The decorator pattern wraps an object in another object that has the same interface and adds behaviour before or after delegating each call. It is a structural pattern from the Gang of Four book (1994). Callers cannot tell whether they hold the original or a wrapped version, and wrappers can be stacked.

```typescript
interface UserStore {
  find(id: string): Promise<User>;
}

class CachedUserStore implements UserStore {
  private cache = new Map<string, User>();
  constructor(private inner: UserStore) {}

  async find(id: string) {
    const hit = this.cache.get(id);
    if (hit) return hit;
    const user = await this.inner.find(id);
    this.cache.set(id, user);
    return user;
  }
}

const store = new LoggedUserStore(new CachedUserStore(new SqlUserStore(db)));
```

The pattern addresses cross-cutting behaviour that would otherwise bloat a class or multiply subclasses. Adding logging, caching and retries by inheritance produces classes such as `CachedLoggedRetryingUserStore`, one for every combination. Decorators let each concern live in a small class that is composed at startup, following the [open-closed principle](./Open-closed%20principle.md) and [composition over inheritance](./Composition%20over%20inheritance.md).

The order of decorators changes behaviour, and this is a usual source of bugs. A retry wrapper outside a cache repeats the cache check on each attempt, while one inside it repeats only the backend call. Logging outside the cache records every request, while logging inside it records only cache misses, which can make traffic graphs look far lower than reality. Build the stack in one place, so the order is explicit and reviewable.

Every wrapper must also delegate the entire interface. A large interface makes this tedious, and a forgotten method bypasses the added behaviour. Deep stacks lengthen stack traces and make debugging harder.

TypeScript's `@decorator` syntax is a related language feature that modifies classes and methods at definition time. It can implement this pattern but is not the same thing: the object pattern composes at runtime, per instance.

A decorator differs from a [proxy](./Proxy%20pattern.md) in intent. A decorator adds behaviour and is usually composed by the caller. A proxy controls access to its subject and often manages that subject's lifecycle.

_Usage:_

"Our request metrics dropped by half after the caching release."

"The logging decorator is now inside the cache, so hits aren't counted. Move it to the outside."
