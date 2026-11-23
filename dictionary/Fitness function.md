---
description: An automated check that measures whether a system still meets a chosen architectural property as it changes.
---

A fitness function is an automated check that measures how well a system meets a chosen architectural property. The term comes from evolutionary computing and was applied to [evolutionary architecture](./Evolutionary%20architecture.md) by Neal Ford, Rebecca Parsons and Patrick Kua in their 2017 book on the subject.

It addresses rules that exist only in documents. A wiki page says the domain layer must not import the database client, everyone agrees, and a year later a search finds forty violations added under deadline. A fitness function fails the build on the first one.

```typescript
import { test, expect } from "vitest";
import { findImports } from "./tools/imports";

test("domain code does not depend on infrastructure", async () => {
  const imports = await findImports("src/domain/**/*.ts");
  const violations = imports.filter((i) => i.target.startsWith("src/infrastructure"));
  expect(violations).toEqual([]);
});
```

| Property     | Example check                                                       | When it runs           |
| ------------ | ------------------------------------------------------------------- | ---------------------- |
| Structure    | No [circular dependencies](./Circular%20dependency.md) between modules | Every build            |
| Performance  | p95 latency stays under a threshold in a load test                  | Nightly or pre-release |
| Security     | No dependency with a known critical vulnerability                   | Every build            |
| Availability | Service survives loss of one instance in a chaos test               | Scheduled              |
| Size         | Frontend bundle stays within a budget                               | Every build            |

Useful fitness functions measure something the team has agreed matters, give a clear failure message and run at a frequency proportional to their cost. A check that fails randomly, or blocks work for a property nobody cares about, gets disabled and then protects nothing. When introducing a rule to an existing codebase, record a baseline of known violations, prevent new ones and reduce the count over time.

Fitness functions enforce decisions but do not make them. Derive each one from a prioritised [quality attribute](./Quality%20attribute.md), and retire it if the goal changes. Run continuously, they also detect [architectural drift](./Architectural%20drift.md) as it happens.

_Usage:_

"We agreed the domain wouldn't import Prisma, and I just found it in six files."

"Add an import check to CI, so the seventh fails the build."
