---
description: Code with tangled control flow, so following what happens next means jumping between many places.
---

Spaghetti code is code whose control flow is so tangled that a reader cannot follow what happens next without jumping between many places. The term dates from unstructured programming, when `goto` could transfer control anywhere. Edsger Dijkstra argued against that style in his 1968 letter "Go To Statement Considered Harmful". Modern code produces the same effect through deep nesting, boolean flags, callbacks, shared mutable state and event handlers that trigger each other.

The symptom appears during debugging. To learn why an order was charged twice, an engineer steps through a function, finds a flag changed halfway down, and then finds that the function calls itself with different arguments.

```typescript
function process(order: Order, retry: boolean, skipTax: boolean) {
  let ok = false;
  if (order.items.length) {
    if (!skipTax) {
      order.tax = calcTax(order);
      if (order.tax < 0) retry = true;
    }
    if (!retry || order.attempts < 3) {
      ok = charge(order);
      if (!ok && retry) return process(order, false, true);
    }
  }
  if (ok) notify(order);
  return ok;
}
```

Because the behaviour is unclear, start by writing tests that record what the code does today. Then simplify in small steps. Use guard clauses to reduce nesting, extract named functions for each stage, and replace boolean parameters with separate functions. When behaviour depends on a status that changes over time, an explicit state machine or the [state pattern](./State%20pattern.md) makes the allowed transitions visible.

Spaghetti code differs from a [big ball of mud](./Big%20ball%20of%20mud.md) in scale. Spaghetti describes control flow inside a function or module, while a big ball of mud describes the structure of a system. A system can have clean module boundaries with one tangled module inside, or tidy functions connected by chaotic dependencies.

Length alone does not make code spaghetti. A hundred-line function that reads from top to bottom can be easier to follow than ten small functions that call each other in a loop. Cyclomatic complexity can flag candidates, but the practical test is whether someone can predict the path through the code without running it.

_Usage:_

"Why was this order charged twice?"

"`retry` changes halfway through and the function calls itself. Let's split it into explicit steps before we fix the bug."
