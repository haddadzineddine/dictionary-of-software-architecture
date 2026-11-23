---
description: A stand-in object with the same interface as another, controlling when and how the real object is accessed.
---

The proxy pattern places a stand-in object in front of another object, called the subject, and gives it the same interface. It is a structural pattern from the Gang of Four book (1994). The proxy receives each call and decides whether, when and how to forward it.

```typescript
interface ReportService {
  generate(id: string): Promise<Report>;
}

class AuthorizedReportService implements ReportService {
  constructor(private real: ReportService, private user: User) {}

  async generate(id: string) {
    if (!this.user.can("reports:read")) throw new ForbiddenError();
    return this.real.generate(id);
  }
}
```

Proxies are commonly grouped by what they control:

| Type            | Controls    | Example                                           |
| --------------- | ----------- | ------------------------------------------------- |
| Virtual         | Creation    | Load a large object on first use                  |
| Protection      | Permission  | Check the caller's rights                         |
| Remote          | Location    | Client stub that calls a service over the network |
| Caching         | Repeat work | Return a stored response                          |
| Smart reference | Bookkeeping | Count references or log access                    |

The main hazard is that a proxy makes expensive or unreliable work look like an ordinary method call. An ORM using [lazy load](./Lazy%20load.md) returns proxy objects, so reading `order.customer.name` in a loop looks harmless but issues one database query per row, and a page gets slower as data grows. A remote proxy has the same problem: a call that reads as local can time out or fail partway. This is a form of [leaky abstraction](./Leaky%20abstraction.md), so make remote and lazy calls visible in names or types where it matters.

JavaScript has a built-in `Proxy` object that intercepts property access and method calls. Libraries use it for reactive state and mocks. It is one way to implement the pattern, but it adds overhead and has identity surprises: a proxy and its target are different objects under `===`, and class private `#fields` throw a `TypeError` when accessed through a proxy.

A proxy differs from a [decorator](./Decorator%20pattern.md) in intent, even though the code can look identical. A decorator adds behaviour and is stacked by the caller. A proxy controls access to its subject and may create or manage that subject itself. An [adapter](./Adapter%20pattern.md) differs by changing the interface, while a proxy keeps it.

Skip a proxy when a plain function call at the boundary does the job, such as a permission check in one handler.

_Usage:_

"This endpoint runs 400 queries to render a list of 400 orders."

"`order.customer` is a lazy proxy. Eager-load customers in the original query."
