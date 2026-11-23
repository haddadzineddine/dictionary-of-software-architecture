---
description: Dividing a program so each part handles one distinct concern, such as presentation, business rules or persistence.
---

Separation of concerns is the practice of dividing a program so that each part deals with one distinct aspect of the problem, such as presentation, business rules or persistence. Edsger Dijkstra used the phrase in a 1974 essay about focusing on one aspect of a problem at a time.

The symptom is a single function that mixes several concerns. A request handler parses JSON, checks permissions, computes a discount, writes SQL and formats an email. Changing the discount requires reading past the SQL, testing it requires an HTTP request and a database, and a copy of the logic appears in the nightly job because it cannot be called on its own.

```typescript
// Mixed: the rule cannot be tested without a request and a database
app.post("/orders", async (req, res) => {
  const user = await db.query("SELECT * FROM users WHERE id = $1", [req.body.userId]);
  const discount = user.rows[0].tier === "gold" ? 0.1 : 0;
  // ...
});

// Separated: the rule is a plain function
function discountFor(tier: Tier): number {
  return tier === "gold" ? 0.1 : 0;
}
```

Concerns can be divided along different axes:

| Axis          | Examples                         |
| ------------- | -------------------------------- |
| Technical     | UI, business logic, data access  |
| Business      | Billing, shipping, catalogue     |
| Cross-cutting | Logging, authentication, caching |

Layered architecture separates on the technical axis, while [package by feature](./Package%20by%20feature.md) separates on the business axis. Many systems use both, with features at the top level. Cross-cutting concerns often go in middleware or a [decorator](./Decorator%20pattern.md).

Separating the wrong things has a cost. Splitting code that always changes together spreads one change across many files, which reduces [cohesion](./Cohesion.md). React components are a familiar example: combining markup and logic in one file was criticised at first as mixing concerns, but in many UIs the markup and its behaviour change together. A practical test for a boundary is whether you can change one side without reading the other.

_Usage:_

"The nightly job has its own copy of the discount logic."

"It's stuck inside the HTTP handler. Pull it out into a plain function and call it from both."
