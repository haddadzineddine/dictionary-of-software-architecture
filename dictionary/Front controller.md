---
description: A single handler that receives every web request, runs shared processing and dispatches to route-specific code.
---

A front controller is a single handler that receives every request to a web application, performs shared processing and dispatches to the code for the specific route. Spring's `DispatcherServlet` and the `public/index.php` entry point in Laravel and Symfony are common examples. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002).

```typescript
async function handle(req: Request): Promise<Response> {
  const session = await authenticate(req);
  const route = router.match(req.method, new URL(req.url).pathname);

  if (!route) return new Response("Not found", { status: 404 });
  if (!route.isAllowed(session)) return new Response("Forbidden", { status: 403 });

  return route.handler(req, session);
}
```

The pattern addresses request handling repeated on every page. When each endpoint performs its own authentication, logging and error formatting, a new admin page can ship without its permission check and remain publicly reachable until someone notices. With a front controller, those steps run for every request by default, and a route has to opt out explicitly.

Most web frameworks apply the pattern implicitly. An Express or Fastify application is a front controller with a router, and its middleware pipeline is a form of [chain of responsibility](./Chain%20of%20responsibility.md). The front controller usually dispatches to [model-view-controller](./Model-view-controller.md) controllers, which handle individual actions.

| Approach         | Entry point              | Cross-cutting logic         | Fits                       |
| ---------------- | ------------------------ | --------------------------- | -------------------------- |
| Page controller  | One per page or endpoint | Repeated or inherited       | Few, independent pages     |
| Front controller | One per application      | Applied centrally           | Most web applications      |
| API gateway      | One for many services    | Applied at the network edge | Multiple deployed services |

Centralisation has trade-offs. A bug in the dispatcher affects every route, and shared steps add latency to endpoints that do not need them, such as health checks. Limit the controller to routing and cross-cutting work, because once it holds business rules or per-route conditionals, it starts to become a [god object](./God%20object.md). Make authorisation deny by default, so that a route missing its configuration fails closed.

The pattern fits less well on platforms that deploy each function separately, since each function has its own entry point. There, shared logic usually moves into a wrapper function applied to each handler.

_Usage:_

"The new reports endpoint was reachable without logging in."

"Auth is applied per route. Move it into the front controller and make public routes opt out."
