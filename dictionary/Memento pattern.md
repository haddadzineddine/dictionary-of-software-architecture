---
description: Capturing an object's state in an opaque snapshot so it can be restored later without exposing its internals.
---

The memento pattern captures an object's internal state in a snapshot that can restore the object later, without exposing that state to other code. It is a behavioural pattern from the Gang of Four book (1994). It has three roles: the originator creates and restores snapshots, the memento holds the state, and the caretaker stores mementos without reading them.

```typescript
class Memento {
  constructor(readonly state: Readonly<{ text: string; cursor: number }>) {}
}

class Editor {
  private text = "";
  private cursor = 0;

  save() {
    return new Memento({ text: this.text, cursor: this.cursor });
  }
  restore(m: Memento) {
    this.text = m.state.text;
    this.cursor = m.state.cursor;
  }
  type(value: string) {
    this.text += value;
    this.cursor += value.length;
  }
}

const history: Memento[] = [];
history.push(editor.save());
editor.type("hello");
editor.restore(history.pop()!);
```

The pattern suits undo, draft recovery, checkpoints in multi-step wizards and rollback after a failed operation. It preserves [encapsulation](./Encapsulation.md): the class that owns the state decides what a snapshot contains, so a history manager does not need access to private fields.

The usual bug is a snapshot that shares references with live state. If a memento stores `this.items` instead of a copy, later edits change the snapshot too, and undo appears to do nothing or restores a half-changed document. Copy mutable state when saving, or keep state immutable so a snapshot can be a reference.

Memory is the second constraint. Saving a large document after each keystroke grows quickly, and long sessions can slow or crash a tab. Cap the history, group rapid changes into one entry, or use structural sharing so that snapshots reuse unchanged data.

Persisted mementos add a versioning problem. A draft saved by last month's release may not match today's shape, so include a schema version and a migration path, or discard old snapshots deliberately. External effects are not restored either: rolling an object back does not unsend an email.

Memento is the alternative to inverse operations in the [command](./Command%20pattern.md) pattern:

| Approach          | Stores                     | Suits                                      |
| ----------------- | -------------------------- | ------------------------------------------ |
| Memento           | Full state                 | Changes that are hard to reverse           |
| Command with undo | The change and its inverse | Large state with small, reversible changes |

The two are often combined, with each command holding a memento of what it altered. For simple state, a plain immutable value in a history array is enough and needs no dedicated classes.

_Usage:_

"Undo restores the title but leaves the edited table cells."

"The snapshot holds a reference to the cells array. Deep-copy it when saving the memento."
