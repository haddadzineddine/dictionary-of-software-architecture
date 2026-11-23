---
description: Passing a request along a sequence of handlers, where each one can handle it, forward it or stop it.
---

Chain of responsibility is a behavioural pattern that passes a request along an ordered sequence of handlers. Each handler decides whether to process the request, pass it to the next handler or stop. The sender knows only the start of the chain. The pattern comes from the Gang of Four book (1994), where a single handler typically takes responsibility for the request. HTTP middleware is a well-known variant in which several handlers each do some work.

```typescript
type Handler = (req: Request, next: () => Promise<Response>) => Promise<Response>;

const auth: Handler = async (req, next) =>
  req.headers.has("authorization") ? next() : new Response("Unauthorized", { status: 401 });

const logging: Handler = async (req, next) => {
  const res = await next();
  console.log(req.url, res.status);
  return res;
};

function chain(handlers: Handler[], final: (req: Request) => Promise<Response>) {
  return (req: Request): Promise<Response> => {
    const run = (i: number): Promise<Response> =>
      i === handlers.length ? final(req) : handlers[i](req, () => run(i + 1));
    return run(0);
  };
}
```

The pattern replaces a long conditional that mixes unrelated checks, such as authentication, rate limiting and validation, in one function. Each check becomes a small unit that can be reordered, reused or tested alone, and new handlers can join the chain without changing the others.

Bugs in a chain usually come from three places:

| Problem                         | Symptom                           | Fix                                     |
| ------------------------------- | --------------------------------- | --------------------------------------- |
| Handler forgets to call `next`  | Request hangs until a timeout     | Always return a response or call `next` |
| Wrong order                     | Validation runs before body parsing | Define the order in one place         |
| No handler matches              | Request is silently dropped       | Add a final default handler             |

A chain also makes control flow harder to read. A developer looking at a route handler cannot see what ran before it, and finding the cause of a 403 may mean walking through several files. Keep chains short and log which handler ended the request.

Chain of responsibility differs from the [decorator](./Decorator%20pattern.md), which has a similar structure. A decorator adds behaviour around one wrapped object and normally still produces its result. A chain handler may reject the request and end processing. It also differs from [pipes and filters](./Pipes%20and%20filters.md), in which each stage transforms data and passes it on, with no handler claiming the request.

For two or three fixed checks, ordinary `if` statements are clearer.

_Usage:_

"Requests to the upload route hang with no error."

"The new quota middleware never calls `next` when the user is under the limit."
