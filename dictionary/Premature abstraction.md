---
description: Merging code into a shared abstraction before enough real cases show what those cases have in common.
---

Premature [abstraction](./Abstraction.md) is the extraction of a shared interface, helper or base class before enough real cases exist to show what they have in common. It usually starts with two similar blocks of code. Someone merges them, a third case differs slightly, and the shared function gains a flag. The symptom is a helper with parameters such as `isInvoice`, `hidePrice` and `legacy`, where a change for one caller breaks another.

```typescript
function renderCard(
  item: Item,
  opts: { compact?: boolean; isInvoice?: boolean; hidePrice?: boolean; legacy?: boolean },
) {
  if (opts.isInvoice && !opts.hidePrice) {
    // Invoice-only layout.
  }
  // Each new caller adds another flag and another branch.
}
```

The usual cause is applying [DRY](./DRY.md) to similar-looking text instead of shared knowledge. Two validation rules can look identical today and change for different business reasons. Merging them creates [coupling](./Coupling.md) between features that had no dependency. The wrong shared code can cost more than duplication, because changing it requires understanding every caller, and engineers tend to keep extending it once it exists.

The rule of three is a common heuristic: wait for three instances before extracting. It is a guide, and these questions are more precise:

| Question                                               | If yes        | If no         |
| ------------------------------------------------------ | ------------- | ------------- |
| Must a change to one case always apply to the others?  | Extract       | Keep separate |
| Can the shared part be named as one clear concept?     | Extract       | Keep separate |
| Would callers need flags to get different behaviour?   | Keep separate | Extract       |

To recover from a bad extraction, inline the shared code back into each caller and delete the branches that caller does not use. Then look at what remains and extract only what is common.

Premature abstraction differs from [speculative generality](./Speculative%20generality.md). Speculative generality builds for imagined future cases, while premature abstraction merges existing cases too early. Duplication is not always acceptable either: when the same business rule is copied and must stay identical, leaving it duplicated leads to [shotgun surgery](./Shotgun%20surgery.md).

_Usage:_

"I need `renderCard` on the invoice page, but it needs another flag."

"That would be the fifth flag. Copy the markup for invoices and we'll see what the two have in common."
