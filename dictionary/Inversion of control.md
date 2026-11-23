---
description: A design where a framework or caller decides when your code runs, instead of your code directing the whole flow.
---

Inversion of control is a design in which a framework or other outside code decides when your code runs, instead of your code directing the program flow. A library is something you call, while a framework calls you. The idea is often summarised as the Hollywood principle: "don't call us, we'll call you".

```typescript
// Your code controls the flow
const input = readRequest();
const result = handle(input);
writeResponse(result);

// The framework controls the flow
app.get("/orders/:id", async (req, res) => {
  res.json(await findOrder(req.params.id));
});
```

In the second example, the server owns the loop, parses the request and handles errors, and your handler runs only when a matching route arrives. Event listeners, React components, test runners and lifecycle hooks work the same way.

The term covers several mechanisms:

| Mechanism                                       | What is inverted             | Example                          |
| ----------------------------------------------- | ---------------------------- | -------------------------------- |
| Callback or event                               | Who triggers the code        | `button.addEventListener`        |
| Framework lifecycle                             | Who owns the main loop       | React rendering a component      |
| [Template method](./Template%20method.md)       | Who controls the steps       | A base class calling hooks       |
| Dependency injection                            | Who creates dependencies     | A constructor receiving a client |
| [Plugin architecture](./Plugin%20architecture.md) | Who decides what gets loaded | A host loading extensions      |

Martin Fowler argued in 2004 that "inversion of control" was too general a label for containers that wire objects together, and proposed the name dependency injection for that case. The two are still often used interchangeably. Inversion of control is the broad idea, dependency injection is one application of it, and the [dependency inversion principle](./Dependency%20inversion%20principle.md) is a separate rule about which way source-code dependencies point.

The benefit is reuse, since a framework solves the general flow and you write only the specific parts. The cost is a flow that is harder to trace. The symptom is a stack trace full of framework internals, or a handler that never runs and reports no error because a registration was missed, with no call site to search for. Where the order of steps matters to the business, as in a payment sequence, keep it in explicit code.

_Usage:_

"Where is this handler called from? I can't find a call site."

"There isn't one. The framework invokes it through the route registration, so start there."
