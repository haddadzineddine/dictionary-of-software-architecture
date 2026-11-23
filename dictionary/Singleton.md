---
description: A class restricted to one instance with a global access point, useful for shared resources but easy to overuse.
---

A singleton is a class that allows only one instance and provides a global point of access to it. It is one of the creational patterns in the Gang of Four book (1994). Its use is disputed, because it solves two problems at once: limiting instances and making an object globally reachable.

```typescript
class Config {
  private static instance?: Config;
  private constructor(readonly databaseUrl: string) {}

  static get(): Config {
    return (Config.instance ??= new Config(process.env.DATABASE_URL!));
  }
}
```

The legitimate motive is a resource that should exist once per process, such as a [connection pool](./Object%20pool.md), a logger or a metrics client. Creating a new database pool per request quickly produces "too many connections" errors. In JavaScript, a module-level `export const db = createPool()` usually achieves this, because a module is evaluated once per resolved path.

That guarantee has limits. Two versions of a package in `node_modules` produce two instances. Development hot reload can re-evaluate the module and open a new pool on every save. Serverless platforms and multi-process deployments have one instance per process, so a singleton is never a cluster-wide guarantee.

The main cost is hidden [coupling](./Coupling.md). A function that calls `Config.get()` does not declare that dependency in its signature. Tests then leak state into one another: a test passes alone and fails when run after another test that changed the shared instance. Mutable singletons behave like global variables, with the same debugging difficulties.

| Approach                        | Instances           | Dependency visible | Easy to replace in tests |
| ------------------------------- | ------------------- | ------------------ | ------------------------ |
| Classic singleton               | One, enforced       | No                 | No                       |
| Module-level instance           | One per module load | No                 | With module mocking      |
| Created at startup and injected | One, by convention  | Yes                | Yes                      |

The usual alternative is to create the object once at application startup and pass it in through dependency injection. This keeps the single instance and removes the global access. A [service locator](./Service%20locator.md) is different again: it centralises lookup, but dependencies stay hidden in the same way.

Stateless, immutable singletons carry little risk and are a reasonable choice.

_Usage:_

"This test only fails when the full suite runs."

"An earlier test changed the `Config` singleton. Inject the config so each test gets its own."
