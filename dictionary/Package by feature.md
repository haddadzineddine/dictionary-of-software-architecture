---
description: Organising code into folders by business capability, instead of by technical layer such as controllers and services.
---

Package by feature is a way of organising source code so that top-level folders represent business capabilities, such as `orders` or `billing`, instead of technical layers such as `controllers` or `services`. Everything one feature needs sits together.

The symptom of the alternative, package by layer, is that a single feature change touches a file in every folder. Adding a field to an order means jumping between `controllers/`, `services/`, `repositories/`, `dtos/` and `validators/`, each holding dozens of unrelated files. The folder tree describes the framework rather than what the application does.

```text
# Package by layer          # Package by feature
src/                        src/
  controllers/                orders/
    orders.ts                   routes.ts
    billing.ts                  place-order.ts
  services/                     order-store.ts
    orders.ts                   index.ts
    billing.ts                billing/
  repositories/                 routes.ts
    orders.ts                   invoice.ts
    billing.ts                  index.ts
```

|                     | By layer                   | By feature                     |
| ------------------- | -------------------------- | ------------------------------ |
| Typical change      | Touches many folders       | Stays in one folder            |
| [Cohesion](./Cohesion.md) | Low, grouped by file type | High, grouped by purpose  |
| Removing a feature  | Search across the tree     | Delete a folder                |
| Team ownership      | Shared across layers       | One team can own a folder      |
| Technical patterns  | Easy to see in one place   | Need shared conventions        |

Folders alone do not create a boundary. Without enforcement, `billing` can import a private file in `orders`, and the features become [coupled](./Coupling.md). Give each feature a public entry point such as `index.ts`, and enforce it with import rules or a tool such as `dependency-cruiser`. Calls between features then go through that interface or through events.

Not everything belongs to a feature. Logging, database connections and design system components go in a small shared area, which should stay free of business logic so it does not become a dumping ground. Layers can still exist inside a feature that is large enough to need them, and small projects can stay flat.

This structure is the folder-level form of [vertical slice architecture](./Vertical%20slice%20architecture.md). It also makes a later move to a modular monolith or a separate service easier, because the boundaries already exist. Feature folders can also match team boundaries, the alignment described by [Conway's law](./Conway's%20law.md).

_Usage:_

"Adding a coupon field meant editing seven folders."

"We're organised by layer. Let's move coupon code into a `coupons` feature folder, behind one `index.ts`."
