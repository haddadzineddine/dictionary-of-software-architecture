---
description: Letting independent specialist components build a solution together by reading and updating a shared data store.
---

The blackboard pattern lets several independent specialist components solve a problem by reading and updating a shared data structure, called the blackboard. A control component chooses which specialist runs next. The pattern originated in the Hearsay-II speech recognition system in the 1970s.

It addresses problems with no known fixed algorithm, where partial results from different kinds of expertise must be combined. In speech recognition, one specialist proposes sounds, another proposes words and another checks grammar. A fixed pipeline struggles here because a later insight may need to revise an earlier guess, which produces a tangle of special cases and backtracking.

| Part              | Responsibility                                              |
| ----------------- | ----------------------------------------------------------- |
| Blackboard        | Holds the problem, partial solutions and hypotheses         |
| Knowledge sources | Each applies one specialism and knows nothing of the others |
| Control           | Selects the next knowledge source from the board's state    |

```typescript
interface KnowledgeSource {
  canContribute(board: Board): boolean;
  contribute(board: Board): void;
}

function solve(board: Board, sources: KnowledgeSource[]) {
  while (!board.isSolved()) {
    const next = sources.find((s) => s.canContribute(board));
    if (!next) throw new Error("No source can make progress");
    next.contribute(board);
  }
  return board.solution();
}
```

Specialists can be added without changing each other, because they communicate only through the board. The costs are those of shared mutable state: the board's schema is a dependency of every specialist, concurrent updates need coordination, and results are hard to reproduce when execution order depends on the data. Termination also needs care, since two specialists can keep revising each other's work.

Do not use the pattern when a deterministic algorithm or a plain pipeline solves the problem. It suits work such as sensor fusion, planning and diagnosis, where the order of steps cannot be fixed in advance.

The blackboard pattern is often confused with the [observer pattern](./Observer%20pattern.md). An observer reacts to notifications from a subject and has no shared goal. A blackboard accumulates a partial solution, and a control strategy directs contributions toward completing it.

_Usage:_

"The fraud rules call each other in an order nobody can follow."

"Have each detector write its findings to a shared case record, and let one controller decide what runs next."
