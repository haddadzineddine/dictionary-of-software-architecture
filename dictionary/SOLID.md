---
description: Five object-oriented design principles, grouped under one acronym, for keeping code easy to change as it grows.
---

SOLID is an acronym for five object-oriented design principles that aim to keep code changeable as it grows. Robert C. Martin gathered the principles, and Michael Feathers proposed the acronym.

| Letter | Principle                                                              | Rule                                               | Violation looks like                         |
| ------ | ---------------------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| S      | [Single responsibility](./Single%20responsibility%20principle.md)      | A module answers to one group of stakeholders      | A billing change breaks a report             |
| O      | [Open-closed](./Open-closed%20principle.md)                            | Add behaviour without editing stable code          | Each payment type edits the same `switch`    |
| L      | [Liskov substitution](./Liskov%20substitution%20principle.md)          | Subtypes honour the parent's contract              | A subclass throws on an inherited method     |
| I      | [Interface segregation](./Interface%20segregation%20principle.md)      | Clients depend only on the methods they use        | A test mocks twenty methods to use two       |
| D      | [Dependency inversion](./Dependency%20inversion%20principle.md)        | Policy depends on [abstractions](./Abstraction.md) | Business rules import the database driver    |

The principles address a common experience: a small feature request touches many unrelated files, and a fix in one place breaks something elsewhere. Each principle targets one source of that [coupling](./Coupling.md), such as a class with too many jobs, a subclass that breaks its parent's contract, or a dependency that points toward a volatile detail.

The principles are heuristics, and applying them mechanically causes a different problem. An interface for every class, a file for every method and several layers of forwarding make a simple flow hard to follow. That outcome is a form of [premature abstraction](./Premature%20abstraction.md). Apply a principle when the code shows the pressure it relieves. Two payment types do not need a plugin system, while a fifth might justify one. [YAGNI](./YAGNI.md) and [KISS](./KISS.md) act as counterweights.

SOLID was written with classes in mind, but most of it carries over to functions and modules in TypeScript. A function type can act as an interface, and a module boundary can hold a single responsibility. Substitution applies to anything with a contract, including an HTTP API whose new version must keep accepting old requests.

_Usage:_

"Should this new class get an interface so it follows SOLID?"

"Only if there's a second implementation or a test that needs one. Otherwise it's an extra file with no benefit."
