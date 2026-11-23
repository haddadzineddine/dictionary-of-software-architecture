---
description: Treating individual objects and groups of objects through one interface by arranging them in a tree.
---

The composite pattern arranges objects in a tree and gives leaves and groups the same interface. It is a structural pattern from the Gang of Four book (1994). A caller can invoke an operation on one item or on an entire subtree without checking which it holds, because each group forwards the call to its children and combines the results.

```typescript
interface FileNode {
  size(): number;
}

class File implements FileNode {
  constructor(private bytes: number) {}
  size() {
    return this.bytes;
  }
}

class Folder implements FileNode {
  private children: FileNode[] = [];
  add(child: FileNode) {
    this.children.push(child);
  }
  size() {
    return this.children.reduce((sum, c) => sum + c.size(), 0);
  }
}
```

The pattern fits data that is naturally hierarchical: file systems, UI component trees, organisation charts, menus, nested permission groups and bundled products in a catalogue. Without it, calling code fills with `if (item.type === "folder")` branches and manual recursion, and each new operation repeats the traversal. A common symptom is logic that handles one or two levels of nesting correctly and breaks when someone creates a third.

The structure has trade-offs. Placing child operations such as `add` on the shared interface makes leaves and groups uniform but forces `File` to implement a method that makes no sense for it, which can violate the [Liskov substitution principle](./Liskov%20substitution%20principle.md). Placing them only on the group, as above, is safer, at the cost of callers needing to know when they hold a group.

Trees also bring operational risks. A cycle, such as a group containing itself through another group, causes infinite recursion and a stack overflow, so reject cycles when adding children. Very deep or very large trees make a simple `size()` call expensive, and results may need caching and invalidation.

A composite differs from a [decorator](./Decorator%20pattern.md), although both forward calls through a shared interface. A decorator wraps exactly one object to add behaviour. A composite holds many children and aggregates their results. To run many unrelated operations across a stable tree, combine it with a [visitor](./Visitor%20pattern.md).

Do not use the pattern for flat lists. An array and a loop are enough.

_Usage:_

"Permissions work for nested groups until someone adds a group inside a group inside a group."

"The check only recurses twice. Model groups as a composite so any depth works."
