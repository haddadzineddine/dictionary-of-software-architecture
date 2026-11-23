---
description: A base class method that fixes an algorithm's steps while subclasses override selected steps.
---

The template method pattern defines the outline of an algorithm in a base class method and lets subclasses supply some of its steps. It is a behavioural pattern from the Gang of Four book (1994). The base class controls the order of the steps, and subclasses override only the ones that vary. Optional steps with a default empty body are called hooks.

```typescript
abstract class DataImport {
  async run(path: string) {
    const raw = await this.read(path);
    const rows = this.parse(raw);
    this.validate(rows);
    await this.save(rows);
    await this.afterSave(rows);
  }

  protected abstract parse(raw: string): Row[];
  protected async afterSave(_rows: Row[]) {} // hook

  private read(path: string) {
    return readFile(path, "utf8");
  }
  private validate(rows: Row[]) { /* shared rules */ }
  private async save(rows: Row[]) { /* shared persistence */ }
}

class CsvImport extends DataImport {
  protected parse(raw: string) {
    return parseCsv(raw);
  }
}
```

The pattern removes duplication among workflows that differ in a few steps. If CSV, JSON and XML imports each copy the same read, validate and save sequence, a fix to validation may reach two of the three, and one format keeps accepting bad rows. With a template method, the sequence exists once. Test frameworks use the same structure for lifecycle methods such as `setUp` and `tearDown`, which the framework calls and a subclass provides. This is a form of [inversion of control](./Inversion%20of%20control.md).

The main cost comes from inheritance. Subclasses depend on the base class's internals and call order, so a small base-class change can break a subclass in a distant file. Reading the flow requires jumping between parent and child. Overrides that must remember to call `super.method()` are a frequent source of bugs, and a class can inherit from only one parent, so two independent variations cannot be combined.

Limit the number of abstract steps, and treat the template itself as non-overridable by convention. TypeScript has no `final` keyword, so a subclass can still replace `run`.

The pattern differs from the [strategy pattern](./Strategy%20pattern.md) in mechanism. A template method varies steps through inheritance, fixed when the class is defined. A strategy varies behaviour through composition and can be swapped at runtime. When variation grows, following [composition over inheritance](./Composition%20over%20inheritance.md) usually means passing the steps as functions:

```typescript
async function runImport(path: string, parse: (raw: string) => Row[]) { /* ... */ }
```

That version is often simpler in TypeScript, so prefer it unless a framework requires subclassing.

_Usage:_

"We fixed the date validation, but XML imports still accept bad dates."

"XML has its own copy of the flow. Move the shared steps into one template and override only parsing."
