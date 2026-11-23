---
description: Designing modules so each one conceals a decision likely to change, keeping that decision out of other modules.
---

Information hiding is the design practice of giving each module a decision that is likely to change and concealing that decision from all other modules. David Parnas introduced it in his 1972 paper "On the Criteria To Be Used in Decomposing Systems into Modules". He argued that modules should be divided by what they hide, rather than by the steps in a processing flow.

The symptom of missing information hiding is a small technical change that spreads widely. Switching the date format, the cache key scheme or a database column means editing dozens of files, because each one learned the detail. When a storage change requires edits in the UI, the storage decision was not hidden.

The details worth hiding are those likely to change:

| Decision                    | Hidden behind                            |
| --------------------------- | ---------------------------------------- |
| Storage engine and schema   | A data access module                     |
| Third-party vendor          | An [adapter](./Adapter%20pattern.md)     |
| Algorithm                   | A function or [strategy](./Strategy%20pattern.md) |
| Data format on disk or wire | A serializer                             |
| Concurrency and caching     | A module's internal implementation       |

```typescript
// Leaks the decision: callers build the key
cache.get(`user:v2:${tenantId}:${userId}`);

// Hides it: the key format can change in one place
userCache.get(tenantId, userId);
```

Information hiding differs from [encapsulation](./Encapsulation.md). Encapsulation is the language-level mechanism of restricting access, such as private fields. Information hiding is the design choice of what to conceal. A class can have only private fields and still leak a decision through a method like `getRedisKey()`, or through a return type that exposes a vendor's objects.

Hiding reduces [coupling](./Coupling.md) and allows modules to be understood and changed independently. It is what makes a [deep module](./Deep%20module.md) possible: a small interface in front of a lot of hidden behaviour. No interface hides everything, because some details show through as latency, failures or ordering, which is the problem described by [leaky abstraction](./Leaky%20abstraction.md). Hiding also requires predicting what will change, so revise boundaries as actual changes show where the pressure is.

_Usage:_

"Why did renaming a cache key touch thirty files?"

"Every caller builds the key itself. Hide the format inside a `userCache` module."
