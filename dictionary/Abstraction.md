---
description: A simplified view of something that exposes what callers need and hides the details they do not need to know.
---

An abstraction is a simplified view of something that keeps the details a user needs and leaves out the rest. A file is an abstraction over disk blocks, an HTTP client is one over sockets, and a `sendInvoice()` function is one over the steps needed to send an invoice. It lets a programmer work with a concept without thinking about how it is implemented.

Abstraction and [information hiding](./Information%20hiding.md) are related but distinct. Abstraction concerns what a caller sees and thinks about. Information hiding concerns which design decisions are kept out of reach. A good interface does both.

Abstractions come in different forms:

| Form                 | Hides                     | Example                    |
| -------------------- | ------------------------- | -------------------------- |
| Function             | Steps of a computation    | `calculateTax(order)`      |
| Data type            | Representation            | `Money` instead of a float |
| Interface            | Which implementation runs | `PaymentGateway`           |
| Module               | Internal structure        | A `billing` package        |
| Protocol or platform | The machinery beneath     | SQL, HTTP, a filesystem    |

A useful abstraction reduces what the reader must know. A poor one adds a name without removing any detail, so the reader has to open it anyway. The symptom is a wrapper whose methods pass through to one call, or a helper such as `fetchData(url, true, false, "legacy")`, where each flag exists because a caller needed something different. A [deep module](./Deep%20module.md) is the favourable shape: a small interface over substantial behaviour.

Abstractions are usually more useful when drawn from several working examples, because the examples show what actually varies. Introduced too early, they encode a guess, which is [premature abstraction](./Premature%20abstraction.md), and later requirements get forced into the wrong shape. Keeping some duplication until the pattern is clear is often cheaper than untangling the wrong design, a trade-off discussed under [DRY](./DRY.md).

No abstraction is complete. Details such as latency or failure can show through, as described under [leaky abstraction](./Leaky%20abstraction.md).

_Usage:_

"This `fetchData` helper has five boolean flags now."

"Each caller wanted something different. Inline it and see what the calls actually have in common."
