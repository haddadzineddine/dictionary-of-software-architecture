---
description: Packages should depend in the direction of stability, so code that is hard to change never relies on code that changes often.
---

The stable dependencies principle says a package should only depend on packages that are more stable than itself. Robert C. Martin defined it as one of his package design principles. "Stable" here means hard to change because many other packages depend on it. It does not mean unchanging.

The symptom is a small edit to a volatile package forcing a large rebuild and retest. A shared `common` package imports a feature package for one helper. Every change to that feature now rebuilds everything that uses `common`, and a minor UI tweak can hold up other teams' releases.

Martin measures this with an instability metric, `I = Ce / (Ca + Ce)`. Ca, or afferent [coupling](./Coupling.md), counts the packages that depend on this one. Ce, or efferent coupling, counts the packages this one depends on. The result runs from 0, stable, to 1, unstable.

| Package        | Ca  | Ce  | I    | Role                                |
| -------------- | --- | --- | ---- | ----------------------------------- |
| `domain-types` | 8   | 0   | 0.00 | Many depend on it, so it changes rarely |
| `billing`      | 2   | 3   | 0.60 | Sits in the middle                  |
| `admin-ui`     | 0   | 5   | 1.00 | Free to change                      |

The rule requires I to decrease along each dependency arrow, as in `admin-ui` to `billing` to `domain-types`.

A stable package is hard to change, so it should not contain things that need frequent change. Martin's companion rule, the stable abstractions principle, says stable packages should be abstract, so they can be extended without being modified, in line with the [open-closed principle](./Open-closed%20principle.md). When a stable package needs something from a volatile one, apply the [dependency inversion principle](./Dependency%20inversion%20principle.md): define an interface in the stable package and implement it in the volatile one.

The metric is a guide. It counts dependencies without weighing them, and a concrete date library can sit at I = 0 without problems because it rarely changes. Use the numbers to find a widely used package that depends on a fast-changing one.

_Usage:_

"Why does a copy change in the admin UI rebuild everything?"

"`common` imports from `admin-ui`. That arrow points at something less stable, so move the helper down."
