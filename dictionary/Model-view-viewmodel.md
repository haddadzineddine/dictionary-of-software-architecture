---
description: A UI pattern where a viewmodel exposes state and commands and the view binds to them declaratively.
---

Model-view-viewmodel, or MVVM, is a user interface pattern in which a viewmodel exposes a screen's state and commands, and the view binds to them declaratively. When the state changes, the binding updates the view, and the viewmodel holds no reference to the view. The pattern came from Microsoft's work on WPF in the mid-2000s and builds on Martin Fowler's Presentation Model.

```typescript
class CartViewModel {
  items = signal<CartItem[]>([]);
  total = computed(() => sum(this.items().map((item) => item.price)));
  canCheckout = computed(() => this.items().length > 0);

  remove(id: string) {
    this.items.update((list) => list.filter((item) => item.id !== id));
  }
}
```

The pattern removes manual UI update code. In [model-view-presenter](./Model-view-presenter.md), each state change needs a call such as `view.showTotal()`, and a forgotten call leaves a stale total. In MVVM, `total` is derived state, so the display follows it. Because the viewmodel has no UI dependency, a test can call `remove()` and assert on `total` without rendering anything.

| Layer     | Holds                                  | Knows about          |
| --------- | -------------------------------------- | -------------------- |
| Model     | Data and business rules                | Neither of the others |
| Viewmodel | Screen state, derived values, commands | The model            |
| View      | Markup and bindings                    | The viewmodel        |

The pattern is common in WPF, in Android with Jetpack's `ViewModel`, and in SwiftUI, and Vue's design was partly inspired by it.

Its failures are harder to trace than explicit calls. Bindings can fail quietly, so a misspelled property in WPF leaves a blank field with no exception, and chains of derived state can trigger update loops or redundant renders. Viewmodels also grow into [god objects](./God%20object.md) when one is created per page and handles every widget on it. Split them by component and keep business rules in the model, since a viewmodel only decides how data is presented.

MVVM differs from [model-view-controller](./Model-view-controller.md), where a controller receives input and selects what to render. In MVVM, input reaches commands through bindings, and rendering follows state. For a small screen or a server-rendered page, a viewmodel is an extra layer with little to test. Many component frameworks already combine these roles using hooks or signals, and a separate class is only needed when the logic is large enough to test alone.

_Usage:_

"The cart total stays stale after removing an item."

"Someone set it by hand in the click handler. Make it a computed value on the viewmodel."
