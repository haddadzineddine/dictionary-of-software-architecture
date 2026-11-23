---
description: A plain object with no business logic that carries data across a boundary such as an API or layer.
---

A data transfer object, or DTO, is a plain object that carries data across a boundary and contains no business logic. Martin Fowler described it in Patterns of Enterprise Application Architecture (2002) as a way to reduce the number of calls to a remote interface by bundling several values into one response. Today the term more often refers to any shape defined for an API request or response, or for a message between layers.

```typescript
type UserResponse = {
  id: string;
  displayName: string;
  joinedAt: string;
};

function toUserResponse(user: User): UserResponse {
  return {
    id: user.id,
    displayName: user.displayName,
    joinedAt: user.joinedAt.toISOString(),
  };
}
```

A DTO separates what a system exposes from how it stores data. Serialising a database [entity](./Entity.md) directly is a common source of incidents: a new `passwordHash` column appears in a JSON response, or a column rename breaks a mobile client that still expects the old field. With a DTO, each exposed field is listed deliberately, and the internal model can change while the contract stays stable.

A request DTO also marks where untrusted input is validated. Parsing the request into a typed shape with a schema library prevents mass assignment, where a client sets a field such as `isAdmin` because the handler passed the entire body to the database.

| Type                                | Has behaviour | Identity              | Purpose                            |
| ----------------------------------- | ------------- | --------------------- | ---------------------------------- |
| DTO                                 | No            | No                    | Carries data across a boundary     |
| [Value object](./Value%20object.md) | Yes           | No, compared by value | Models a domain concept            |
| Entity                              | Yes           | Yes                   | Models something tracked over time |

DTOs cost mapping code, and each new field is touched in several places. For an internal tool where one team owns the API and the table and changes them together, separate DTOs may add boilerplate with little protection. Where an API has external consumers, the separation is usually worth it. Keep rules out of DTOs, because pricing logic placed on a response type is invisible to anyone reading the [domain model](./Domain%20model.md).

_Usage:_

"Why is `passwordHash` in the profile response?"

"The handler serialises the user row. Return a `UserResponse` DTO that lists only the public fields."
