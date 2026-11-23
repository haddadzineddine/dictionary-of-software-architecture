---
description: A structure where a host application defines extension points and separately packaged modules add behaviour.
---

A plugin architecture is a structure in which a host application defines extension points, and separately packaged modules add behaviour by implementing them. The host does not know at compile time which plugins exist. It discovers or receives them through configuration and calls them at defined moments. VS Code extensions, ESLint rules and webpack plugins work this way.

```typescript
type BuildHook = (files: File[]) => File[];

interface Plugin {
  name: string;
  setup(host: { onBuild(hook: BuildHook): void }): void;
}

function loadPlugins(plugins: Plugin[]) {
  const hooks: BuildHook[] = [];
  for (const plugin of plugins) {
    plugin.setup({ onBuild: (hook) => hooks.push(hook) });
  }
  return (files: File[]) => hooks.reduce((acc, hook) => hook(acc), files);
}
```

The pattern addresses features that vary by customer, environment or community. Without it, the main codebase fills with branches such as `if (customer === "acme")`, and each new integration requires a change and a release of the host. With extension points, new behaviour ships as a new module, which applies the [open-closed principle](./Open-closed%20principle.md) at application level. The host calls the plugin, a form of [inversion of control](./Inversion%20of%20control.md).

The plugin API becomes a public contract, and this is the main cost. Hooks, arguments and lifecycle details that plugins rely on are hard to change, and a host upgrade that alters them breaks plugins the team has never seen.

| Concern           | Failure                                  | Mitigation                                |
| ----------------- | ---------------------------------------- | ----------------------------------------- |
| Versioning        | An upgrade breaks installed plugins      | Version the API and declare compatibility |
| Ordering          | Plugins conflict depending on load order | Define explicit phases                    |
| Failure isolation | One plugin crashes the host              | Catch errors or use a separate process    |
| Security          | Third-party code has host permissions    | Sandbox or restrict capabilities          |
| Performance       | Slow plugins delay startup               | Load on demand and measure                |

Avoid this structure when the variation is hypothetical. Building extension points before a second implementation exists is [speculative generality](./Speculative%20generality.md), and the resulting API is likely to be wrong. Extract extension points from real cases.

A plugin architecture differs from [microkernel architecture](./Microkernel%20architecture.md). In a microkernel, the host is a minimal system and most functionality, including essential features, is delivered as plugins. A plugin architecture can also describe a complete application with optional extensions.

_Usage:_

"Another customer wants a custom export format."

"Stop adding branches to the exporter. Define an export hook and ship this format as a plugin."
