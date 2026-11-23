---
description: Creating new objects by copying an existing instance instead of constructing them from scratch.
---

The prototype pattern creates new objects by copying an existing instance, called the prototype, instead of constructing each one from scratch. It is a creational pattern from the Gang of Four book (1994). Each prototype exposes a `clone()` method, so code can duplicate an object without knowing its concrete class.

```typescript
interface Cloneable<T> {
  clone(): T;
}

class ChartConfig implements Cloneable<ChartConfig> {
  constructor(
    public title: string,
    public series: string[],
    public colors: Map<string, string>,
  ) {}

  clone() {
    return new ChartConfig(this.title, [...this.series], new Map(this.colors));
  }
}

const base = new ChartConfig("Revenue", ["2025"], new Map([["2025", "blue"]]));
const copy = base.clone();
copy.series.push("2026"); // base is unaffected
```

The pattern is useful when setup is expensive or involves many steps, such as an object configured from a parsed file, or when users duplicate existing items in an editor. A preconfigured instance becomes the starting point, and each copy changes only what differs.

The main failure is the shallow copy. A spread such as `{ ...config }` copies only the top level, so nested arrays and objects remain shared. A user edits the duplicated chart and the original changes too. Each `clone()` must decide which fields are copied and which are deliberately shared.

Generic deep-copy tools have limits. `structuredClone` handles nested data and cycles, but it throws on functions and returns class instances as plain objects without their methods. Objects that hold sockets, file handles or database connections should not be copied at all, and identifiers often need to be regenerated so the copy is not mistaken for the original.

The name overlaps with JavaScript's prototype chain, but they are different mechanisms. The language feature shares behaviour by delegating property lookups to another object. The pattern makes an independent copy of state.

Avoid the pattern when a constructor or [builder](./Builder%20pattern.md) can produce the object cheaply. Copying adds a second way to create objects, and every new field must be remembered in `clone()`. A forgotten field appears as a duplicate that silently loses a setting.

_Usage:_

"Duplicating a dashboard and editing it changes the original as well."

"The clone is shallow, so both share the same widgets array. Copy the nested state in `clone()`."
