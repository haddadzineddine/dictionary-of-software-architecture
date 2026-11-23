---
description: How closely the contents of a module belong together, judged by whether they serve one purpose and change for one reason.
---

Cohesion is the degree to which the elements inside a module belong together. A highly cohesive module has one clear purpose, and its parts change for the same reasons. Like [coupling](./Coupling.md), the term comes from Larry Constantine's structured design work. The two are usually discussed together, since modular design aims for high cohesion within modules and low coupling between them.

The symptom of low cohesion is a module you cannot describe without using "and", or a file named `utils.ts`, `helpers.ts` or `common.ts` that every other file imports. A change to one feature requires opening five folders, the files you open are mostly unrelated code, and unrelated work conflicts during merges.

The structured design scale ranks types of cohesion from weakest to strongest:

| Type            | Parts are grouped because       | Example                           |
| --------------- | ------------------------------- | --------------------------------- |
| Coincidental    | No real reason                  | `utils.ts`                        |
| Logical         | Same category of thing          | All validators in one file        |
| Temporal        | They run at the same time       | `startup()` does unrelated setup  |
| Procedural      | They run in sequence            | Steps in a long workflow function |
| Communicational | They use the same data          | Functions that all read a `Report` |
| Sequential      | One's output feeds the next     | Parse, then transform             |
| Functional      | They all contribute to one task | A `TaxCalculator`                 |

To raise cohesion, move code next to the code it changes with. [Package by feature](./Package%20by%20feature.md) does this at the folder level, by placing a feature's routes, logic and queries together rather than scattering them across technical layers. At class level, the [single responsibility principle](./Single%20responsibility%20principle.md) applies the same idea, and [feature envy](./Feature%20envy.md) is a sign that a method sits in the wrong class.

Cohesion and file size are separate matters. A 600-line module that does one thing may be more cohesive than six 100-line files that must be read together, and splitting it can make things worse. Ask whether a typical change stays within the module. If it does, the boundary is working.

_Usage:_

"`utils.ts` is 2,000 lines and everyone conflicts in it."

"Nothing in there is related. Move each helper next to the feature that uses it."
