---
description: Building a system from a minimal kernel with features supplied by plug-ins that connect through a stable contract.
---

Microkernel architecture builds a system around a minimal kernel that provides only essential services, with other functionality delivered by plug-in modules. The term comes from operating systems such as Mach and MINIX, where services such as file systems run outside the kernel. At application level, the same structure appears in IDEs and in products extended per customer.

The style addresses a product whose variations have accumulated inside its main code. The symptom is branches such as `if (customer === "acme")` in billing logic, with each new client adding risk for all the others. A microkernel moves those variations behind a contract.

```typescript
interface Plugin {
  name: string;
  register(host: Host): void;
}

class Host {
  private handlers = new Map<string, (doc: Doc) => Doc>();

  addHandler(type: string, fn: (doc: Doc) => Doc) {
    this.handlers.set(type, fn);
  }

  load(plugins: Plugin[]) {
    for (const plugin of plugins) plugin.register(this);
  }
}
```

The kernel handles loading, the plug-in lifecycle and shared services such as configuration and logging. Plug-ins depend on the kernel's contract and ideally not on each other. That contract becomes a public API, so changing it can break every plug-in, including third-party ones. Version it and keep it small. A faulty plug-in can also crash the host unless it runs in a separate process or sandbox, which adds communication overhead.

Avoid the style when a product has few expected variations. Building an extension system for two known cases adds a contract to maintain and is a form of [speculative generality](./Speculative%20generality.md).

Microkernel architecture overlaps with [plugin architecture](./Plugin%20architecture.md), which describes the general technique of extending an application through plug-ins. A microkernel is the stricter form: the kernel is deliberately minimal, and much of the product's standard functionality is itself built as plug-ins. An application that accepts a few plug-ins around a large built-in feature set has a plugin architecture but not a microkernel.

_Usage:_

"Every new customer adds another branch to the billing code."

"Keep the billing engine small and ship each customer's rules as a plug-in."
