---
description: A module should have one reason to change, meaning it answers to one group of people with one kind of need.
---

The single responsibility principle says a module should have one reason to change. Robert C. Martin, who named it as part of [SOLID](./SOLID.md), later restated it as a module being responsible to one actor, meaning one group of stakeholders who request changes.

The principle is often misread as "a class should do one thing", which leads to many tiny classes. The actual test concerns who drives change. A class can have several methods and still satisfy the principle if one group's needs determine all of them.

The symptom is a change for one team breaking behaviour for another. Finance asks for a new overtime calculation, a developer edits the shared `regularHours()` helper, and an HR report that relied on the old figure changes without anyone noticing. Both groups' requirements meet in the same code, so unrelated work also produces merge conflicts.

```typescript
// Three actors, one class
class Employee {
  calculatePay() {} // finance
  reportHours() {} // HR
  save() {} // platform team
}
```

The usual fix is to split by actor into `PayCalculator`, `HoursReporter` and `EmployeeStore`, each working on shared employee data. A [facade](./Facade%20pattern.md) can keep one entry point for callers that want it.

Splitting has a cost. Code that always changes together belongs together, and separating it creates [shotgun surgery](./Shotgun%20surgery.md), where one change touches many files. Aim for high [cohesion](./Cohesion.md): group what changes for the same reason and separate what changes for different reasons. At the other extreme, a class that keeps accumulating responsibilities becomes a [god object](./God%20object.md).

Apply the principle when you see the pressure, such as two teams repeatedly editing one file. A small class with a single user does not need splitting because it could one day have two.

_Usage:_

"Why did the payroll fix change the numbers on the HR dashboard?"

"Both use the same hours method on `Employee`. That's two reasons to change in one class, so let's split it."
