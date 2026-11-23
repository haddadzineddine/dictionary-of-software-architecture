---
description: Dead or obsolete code that stays in production because nobody knows whether it is safe to remove.
---

Lava flow is dead or obsolete code that stays in a system because nobody knows whether removing it is safe. The name, used in the 1998 book _AntiPatterns_, compares this code to lava that has cooled and hardened, so later work builds on top of it. It shows up as files named `handler_old` or `pricing_v2`, a config flag nobody can explain, and a comment reading "do not delete, not sure why".

This code usually comes from experiments and migrations that were never finished. A strangler fig migration that stops halfway, for example, leaves two paths in production. The original authors move on, and each later engineer leaves the code alone because deleting it might break something.

Keeping it has a continuing cost and forms part of a system's [technical debt](./Technical%20debt.md). Engineers read and maintain code that does nothing, searches return false leads, and libraries used only by dead code still need security patches. Dormant paths can also be triggered by accident.

Removal is safe when it follows a sequence of checks:

| Step    | What to do                                                            |
| ------- | --------------------------------------------------------------------- |
| Search  | Find references, including reflection, dynamic imports and config     |
| Observe | Add a log or metric to the path and watch a full business cycle       |
| Disable | Put the path behind a flag and switch it off in production            |
| Delete  | Remove the code, knowing version control keeps the history            |
| Prevent | Give each experiment and migration an owner and a removal date        |

The observation period matters because some code runs rarely. A path that looks unused for three weeks may belong to a month-end or year-end job.

Old code is not automatically lava flow. Legacy code that is in use and understood is simply legacy code. Lava flow also differs from [speculative generality](./Speculative%20generality.md), which is code built for a future need that never arrived. Lava flow is usually left behind by past work that was abandoned or replaced.

_Usage:_

"Can we delete `pricing_v2`? I can't find anything that calls it."

"The quarter-end job loads modules by name. Add a log and wait until that job has run."
