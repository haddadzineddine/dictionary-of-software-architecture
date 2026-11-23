---
description: A module with a small interface hiding a large amount of functionality, so callers get much behaviour for little knowledge.
---

A deep module is one whose interface is small compared with the functionality behind it. John Ousterhout uses the term in _A Philosophy of Software Design_, weighing what a module provides against the complexity of its interface. A shallow module is the opposite: its interface is nearly as complicated as its implementation.

Unix file I/O is Ousterhout's standard example. Five calls, `open`, `read`, `write`, `lseek` and `close`, hide file layout, caching, permissions and disk scheduling.

The symptom of shallow modules is a call stack of methods that each do very little. To trace one request you open a controller, a service, a manager and a helper, each forwarding arguments to the next. Every layer adds a name and a signature to learn while hiding almost nothing. Splitting code into many tiny classes and functions often makes this worse.

```typescript
// Shallow: callers must know the steps and their order
const conn = await pool.acquire();
const stmt = await conn.prepare(sql);
const rows = await stmt.execute(params);
await stmt.close();
pool.release(conn);

// Deep: pooling, preparation and cleanup are hidden
const result = await db.query(sql, params);
```

|                      | Shallow                      | Deep                       |
| -------------------- | ---------------------------- | -------------------------- |
| Interface            | Wide, mirrors the internals  | Narrow, describes the task |
| Caller must know     | Steps, order, edge cases     | What they want done        |
| Changes to internals | Often reach callers          | Stay inside                |
| Testing              | Many mocks of internal parts | Test through the interface |

Deep modules are built through [information hiding](./Information%20hiding.md). Pull complexity downward, so the module handles retries, defaults and edge cases rather than pushing them to every caller. Merging two shallow classes that always change together often produces one deeper class and raises [cohesion](./Cohesion.md).

Depth has limits. A module that hides too much can stop callers doing what they need, so keep common cases simple and offer an optional lower-level path for rare ones. A large module with unrelated contents is a [god object](./God%20object.md), because depth comes from one purpose with much behind it and not from size alone.

_Usage:_

"To send an email I have to build a transport, a template and a retry policy first."

"That module is shallow. Give it one `send(to, template, data)` and keep the rest inside."
