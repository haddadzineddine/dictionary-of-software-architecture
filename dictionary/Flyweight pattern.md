---
description: Saving memory by sharing the immutable parts of many similar objects and passing the varying parts in at use.
---

The flyweight pattern reduces memory use by sharing the common, immutable state of many similar objects. It is a structural pattern from the Gang of Four book (1994). The pattern divides each object's data in two: intrinsic state, which is identical across many objects and can be shared, and extrinsic state, which varies per use and is stored by the caller or passed in.

```typescript
class TreeType {
  constructor(readonly species: string, readonly texture: Uint8Array) {}
  draw(x: number, y: number) { /* render texture at x, y */ }
}

class TreeTypes {
  private types = new Map<string, TreeType>();

  get(species: string, load: () => Uint8Array) {
    let type = this.types.get(species);
    if (!type) {
      type = new TreeType(species, load());
      this.types.set(species, type);
    }
    return type;
  }
}

const trees = [{ x: 10, y: 20, type: types.get("oak", loadOak) }];
```

The pattern addresses programs that run out of memory because they hold large numbers of near-identical objects. A map with a million markers, each carrying its own copy of an icon, or a text editor storing font data per character, can crash a browser tab or trigger long garbage collection pauses. Sharing one `TreeType` across a million trees leaves each tree holding only coordinates and a reference.

Shared state must be immutable. If one caller mutates a flyweight, every object using it changes at once, and the bug appears in an unrelated part of the screen. Mark fields `readonly` and freeze objects where appropriate.

The pattern has costs. The factory's cache can grow indefinitely if keys are unbounded, creating a leak while trying to save memory. Code becomes harder to follow because an object's data now lives in two places, and computing extrinsic state on each call can cost CPU time.

Measure with a heap profile before applying it. If there are thousands of objects rather than millions, or little data is actually duplicated, the pattern adds complexity for a negligible saving.

A flyweight differs from an [object pool](./Object%20pool.md). A pooled object is mutable and used by one borrower at a time, while a flyweight is used by many at the same moment. It also differs from a [singleton](./Singleton.md), which has one instance overall, whereas a flyweight factory holds one instance per distinct key.

_Usage:_

"The map tab dies at around 200,000 markers."

"Each marker holds its own copy of the icon bitmap. Share one flyweight per icon type and store only positions."
