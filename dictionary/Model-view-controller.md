---
description: A user interface pattern dividing code into a model for data, a view for display and a controller for input.
---

Model-view-controller, or MVC, is a pattern that divides a user interface into three roles: the model holds data and rules, the view displays it, and the controller handles input. Trygve Reenskaug devised it for Smalltalk at Xerox PARC in the late 1970s. The aim was to let the same data be displayed in several ways and to keep presentation code apart from application logic, an early form of [separation of concerns](./Separation%20of%20concerns.md).

| Role       | Responsibility                    | Should not                  |
| ---------- | --------------------------------- | --------------------------- |
| Model      | Holds state and business rules    | Know how it is displayed    |
| View       | Renders the model                 | Contain business rules      |
| Controller | Translates input into model calls | Hold business logic         |

The name now describes two different designs. In the original desktop form, views subscribed to the model through the [observer pattern](./Observer%20pattern.md), so a model change updated every view. In server-side web frameworks such as Rails and Spring MVC, a controller handles an HTTP request, loads data and renders a template once, with no ongoing observation. Many disagreements about what MVC means come from mixing these two.

```typescript
class ArticlesController {
  constructor(private articles: ArticleStore, private view: ArticleView) {}

  async show(req: AppRequest) {
    const article = await this.articles.get(req.params.id);
    return article ? this.view.render(article) : notFound();
  }
}
```

The most frequent failure is the fat controller. Validation, pricing and email sending accumulate in action methods because the controller is the first place a developer can reach, and the same logic must then be copied to the API or a background job. Move that work to a [service layer](./Service%20layer.md) or onto domain objects, and leave the controller to parse input and choose a response.

MVC is a presentation pattern and does not describe a full application. A codebase with `models/`, `views/` and `controllers/` folders can still have no clear structure in its business logic. The related [model-view-presenter](./Model-view-presenter.md) and [model-view-viewmodel](./Model-view-viewmodel.md) patterns change how the view and the logic communicate, mainly to make UI logic easier to test.

_Usage:_

"The checkout action is 400 lines, and the mobile API has a copy of it."

"Extract the logic into a service so both controllers only handle input and output."
