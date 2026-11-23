---
description: Clients should not depend on methods they do not use, so large interfaces are split into smaller ones per client.
---

The interface segregation principle says that no client should be forced to depend on methods it does not use. Instead of one large interface, define smaller ones shaped around what each caller needs. It is the I in [SOLID](./SOLID.md), formulated by Robert C. Martin.

The symptom is a test that stubs twenty methods so a function can call two of them, or a change to an unrelated method that forces a rebuild of code that never calls it. Implementers are affected too. A class may have to write `throw new Error("not supported")` for methods that make no sense for it, which also breaks the [Liskov substitution principle](./Liskov%20substitution%20principle.md).

```typescript
interface UserStore {
  findById(id: string): Promise<User>;
  search(query: string): Promise<User[]>;
  save(user: User): Promise<void>;
  delete(id: string): Promise<void>;
  exportAll(): Promise<Buffer>;
}

// This consumer names only what it needs
type UserReader = Pick<UserStore, "findById">;

async function greeting(users: UserReader, id: string) {
  const user = await users.findById(id);
  return `Hello, ${user.name}`;
}
```

TypeScript makes this inexpensive because its types are structural. A function can declare a narrow parameter type with `Pick` or an inline interface, and any object with those methods satisfies it, with no change to the concrete class. A test can then pass a small object with one method.

Narrow interfaces reduce [coupling](./Coupling.md) and document what a function actually uses. The principle differs from the [single responsibility principle](./Single%20responsibility%20principle.md) in viewpoint: single responsibility concerns why an implementation changes, while segregation concerns what a caller can see. One class may legitimately implement several narrow interfaces.

Over-applied, the principle produces a one-method interface per call site and many near-identical types. Split where consumers genuinely differ. An interface that its callers use in full should stay whole, and a [deep module](./Deep%20module.md) with a small interface often avoids the problem from the start.

_Usage:_

"This test mocks the whole `UserStore` just to read one user."

"The function only calls `findById`. Narrow its parameter to that and the test needs a one-line stub."
