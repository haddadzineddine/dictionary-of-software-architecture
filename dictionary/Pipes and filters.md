---
description: Processing a data stream through independent steps, where each filter transforms input and passes output along a pipe.
---

Pipes and filters is an architecture style that splits processing into a sequence of independent steps. Each filter reads input, transforms it and writes output. Each pipe carries that output to the next filter. Unix shell pipelines are a familiar example: `grep error app.log | sort | uniq -c`.

The style addresses processing code that has grown into one long function. An import job that parses, validates, normalises, enriches and writes in a single 400-line procedure is hard to test, and adding a step means reading all of it. Splitting the work gives each step one input, one output and no knowledge of its neighbours.

```typescript
type Filter<I, O> = (input: AsyncIterable<I>) => AsyncIterable<O>;

const parse: Filter<string, Row> = async function* (lines) {
  for await (const line of lines) yield JSON.parse(line);
};

const onlyPaid: Filter<Row, Row> = async function* (rows) {
  for await (const row of rows) if (row.status === "paid") yield row;
};

const output = onlyPaid(parse(readLines("orders.jsonl")));
```

Filters share only a data format, so they can be tested alone, reused and reordered where their formats allow. Streaming implementations can run stages concurrently and scale a slow stage independently. Bounded pipes provide backpressure, which stops a fast producer exhausting memory while a slow consumer catches up.

The style fits poorly when steps need shared state or interactive request and response. A filter that needs a value computed three stages earlier forces extra fields through every pipe. Error handling also needs a decision: a malformed record can stop the pipeline, be skipped, or go to a dead-letter location for inspection. Transactions spanning several filters are hard to provide, so make each stage idempotent where a job may be retried.

Pipes and filters is often confused with [chain of responsibility](./Chain%20of%20responsibility.md). In a chain, each handler decides whether to handle a request or pass it on, and the request may stop early. In a pipeline, every filter normally processes each item and contributes to the transformed output.

_Usage:_

"The import fails somewhere in a 500-line function and we can't test any of it."

"Split it into parse, validate and load filters, then test each one with sample rows."
