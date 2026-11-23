---
description: Constructing a complex object step by step through a separate builder, then producing it with a final call.
---

The builder pattern separates the construction of a complex object from the object itself. A builder collects values through a series of method calls, and a final `build()` call validates them and returns the finished object. The Gang of Four book (1994) describes the pattern with a director that runs the steps. Much modern code drops the director and chains calls on the builder.

```typescript
class HttpRequestBuilder {
  private headers: Record<string, string> = {};
  private timeoutMs = 5000;
  private body?: string;

  constructor(private url: string) {}

  header(name: string, value: string) {
    this.headers[name] = value;
    return this;
  }

  timeout(ms: number) {
    this.timeoutMs = ms;
    return this;
  }

  json(data: unknown) {
    this.body = JSON.stringify(data);
    return this.header("Content-Type", "application/json");
  }

  build(): HttpRequest {
    if (this.timeoutMs <= 0) throw new Error("timeout must be positive");
    return new HttpRequest(this.url, { ...this.headers }, this.timeoutMs, this.body);
  }
}
```

The pattern addresses constructors with long parameter lists. A call such as `new Report(id, true, false, null, 30, "pdf")` is hard to read, and swapping two booleans compiles and produces the wrong report. Named builder steps make each value visible, and `build()` gives cross-field rules one place to run, so a half-configured object does not reach the rest of the program.

In TypeScript, an options object usually solves the same problem with less code:

```typescript
new Report({ id, includeCharts: true, format: "pdf" });
```

Use a builder when construction has real steps: values depend on earlier ones, rules span several fields, or the object is assembled across different functions. Query builders and test data builders are common examples. A test builder supplies valid defaults, so each test states only the field it cares about.

A mutable builder has one recurring hazard. Reusing the same instance for two objects can carry headers or filters from the first into the second, so either create a new builder each time or have each step return a copy.

The builder differs from a [factory method](./Factory%20method.md). A factory produces an object in one call and chooses which type to create. A builder assembles one object over several calls and focuses on how it is configured.

_Usage:_

"Why did forty tests break when we added a required field to `Order`?"

"Every test constructs it by hand. Add an order builder with valid defaults and only override what each test needs."
