---
description: Providing a standard way to traverse a collection one element at a time without exposing its internal structure.
---

The iterator pattern provides a way to access the elements of a collection in sequence without exposing how the collection is stored. It is a behavioural pattern from the Gang of Four book (1994). An iterator tracks the current position and hands out one element at a time, so the same loop can work over an array, a tree, a file or a paginated API.

JavaScript builds the pattern into the language. An object is iterable if it has a `Symbol.iterator` method, and generator functions produce iterators with little code. `for...of`, array spread and array destructuring all use this protocol.

```typescript
async function* allOrders(api: OrdersApi) {
  let cursor: string | undefined;
  do {
    const page = await api.list({ cursor, limit: 100 });
    yield* page.items;
    cursor = page.nextCursor;
  } while (cursor);
}

for await (const order of allOrders(api)) {
  if (order.total > 10_000) {
    flag(order);
    break;
  }
}
```

A common reason to use an iterator is a job that loads an entire table or API result into an array and runs out of memory once the data grows. An iterator fetches one page at a time, holds little in memory and can stop early: the `break` above means later pages are never requested.

Iterators have a few recurring surprises:

| Behaviour                       | Symptom                                                            |
| ------------------------------- | ------------------------------------------------------------------ |
| Generators are single-use       | A second loop over the same object yields nothing                  |
| Evaluation is lazy              | Errors appear during iteration, not where the iterator was created |
| Source changes during traversal | Elements are skipped or repeated                                   |
| Early exit needs cleanup        | A file or cursor stays open unless `finally` releases it           |

The last row has a language-level answer: `for...of` calls the iterator's `return` method on `break`, which runs any `finally` block in a generator.

An iterator differs from a [visitor](./Visitor%20pattern.md). An iterator controls the order of traversal and leaves the work to the caller. A visitor defines per-type operations that run over a structure, and the traversal can be kept elsewhere.

Exposing an iterator also helps [encapsulation](./Encapsulation.md): a class can offer iteration over its items without returning the private array, which callers could mutate.

Skip custom iterators for small in-memory arrays, where `map` and `filter` are clearer.

_Usage:_

"The export job gets OOM-killed now that we have two million rows."

"It loads them all first. Iterate with a cursor and write one batch at a time."
