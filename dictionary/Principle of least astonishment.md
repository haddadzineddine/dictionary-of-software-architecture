---
description: A component should behave the way its users expect, so that names, defaults and results do not surprise them.
---

The principle of least astonishment says a component should behave in the way most of its users expect. It applies to API design, naming, defaults, configuration and user interfaces. When behaviour and expectation differ, the design is usually the thing to change.

The symptom is a bug caused by a reasonable assumption. JavaScript's `sort()` compares values as strings by default, so `[10, 9, 1].sort()` returns `[1, 10, 9]`. Application code produces the same kind of surprise:

| Surprise                                 | Expectation                    | Fix                       |
| ---------------------------------------- | ------------------------------ | ------------------------- |
| `delete()` only archives                 | The record is gone             | Name it `archive()`       |
| `getUser()` writes to the database       | Reads have no effects          | Separate the write        |
| The default is to retry forever          | Calls eventually fail          | Use a bounded default     |
| One parser throws, another returns `null` | Errors work the same way      | Pick one convention       |
| A CLI flag deletes without confirmation  | Destructive actions ask first  | Require explicit consent  |

Expectation depends on the audience. The conventions of the language, framework and codebase set what users assume, so an API should follow them even where a different design might be slightly better in isolation. A method named `map` should behave like `map` everywhere else in that language.

Surprises cost the most at boundaries that are hard to change, such as a public API, a CLI or a library. After release, callers come to depend on the surprising behaviour, so correcting it becomes a breaking change. Review names and defaults before publishing them.

Apply the principle by making side effects visible in names, choosing safe defaults and staying consistent with neighbouring code. [Command-query separation](./Command-query%20separation.md) removes one common source of surprise, and a shared [ubiquitous language](./Ubiquitous%20language.md) reduces another by keeping names aligned with what the business means. Where unusual behaviour is necessary, document it at the point of use.

_Usage:_

"I called `user.delete()` and the row is still there."

"It soft-deletes. That surprises everyone, so let's rename it `archive()` before more code depends on it."
