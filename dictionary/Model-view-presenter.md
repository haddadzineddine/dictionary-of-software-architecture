---
description: A UI pattern where a presenter holds presentation logic and updates a passive view through an interface.
---

Model-view-presenter, or MVP, is a user interface pattern in which a presenter holds the presentation logic and communicates with a view through an interface. The view forwards user actions to the presenter and displays what it is told. The model holds data and business rules, and the view does not access it directly. The pattern emerged in the 1990s and became common in Windows Forms and Android applications.

```typescript
interface LoginView {
  showError(message: string): void;
  goToDashboard(): void;
}

class LoginPresenter {
  constructor(private view: LoginView, private auth: Auth) {}

  async submit(email: string, password: string) {
    const ok = await this.auth.signIn(email, password);
    if (ok) this.view.goToDashboard();
    else this.view.showError("Incorrect email or password");
  }
}
```

The pattern addresses UI logic that can only be tested through the UI. When a screen's rules live in an Android `Activity` or a form class, checking that a failed login shows an error requires launching the screen, and such tests are slow and flaky. With a presenter, a test passes a fake `LoginView` and asserts that `showError` was called, with no rendering involved.

MVP differs from its neighbours in how the view receives updates:

| Pattern                                             | Who handles input          | How the view updates         | View knows about |
| --------------------------------------------------- | -------------------------- | ---------------------------- | ---------------- |
| [MVC](./Model-view-controller.md)                   | Controller                 | Observes or is rendered      | Model            |
| MVP                                                 | View forwards to presenter | Presenter calls view methods | Presenter        |
| [MVVM](./Model-view-viewmodel.md)                   | View binds to commands     | Data binding to state        | Viewmodel        |

Martin Fowler separated two variants. In Passive View, the presenter sets every field, so the view contains almost no logic. In Supervising Controller, the view handles simple data binding and the presenter handles the complicated cases.

The main costs are boilerplate and presenter size. Each screen needs a view interface and manual update calls, and one forgotten call leaves the screen out of sync with its state. Presenters can also grow into [god objects](./God%20object.md) on complicated screens, so split them by component. In frameworks with reactive binding, MVVM or plain components usually need less code, and MVP is mostly seen in existing codebases.

_Usage:_

"Testing the login error means booting an emulator."

"Move the logic to a presenter behind a `LoginView` interface, then test it with a fake view."
