---
description: Representing a small language's grammar as classes so that expressions in that language can be evaluated.
---

The interpreter pattern represents the grammar of a small language as a set of classes, one per rule, and evaluates sentences in that language by walking a tree of those objects. It is a behavioural pattern from the Gang of Four book (1994). Expressions form an abstract syntax tree, and each node implements an `interpret` method that uses a shared context.

```typescript
type Context = Record<string, number>;

interface Expr {
  interpret(ctx: Context): boolean;
}

class GreaterThan implements Expr {
  constructor(private field: string, private value: number) {}
  interpret(ctx: Context) {
    return ctx[this.field] > this.value;
  }
}

class And implements Expr {
  constructor(private left: Expr, private right: Expr) {}
  interpret(ctx: Context) {
    return this.left.interpret(ctx) && this.right.interpret(ctx);
  }
}

// age > 18 AND score > 700
const rule = new And(new GreaterThan("age", 18), new GreaterThan("score", 700));
rule.interpret({ age: 30, score: 720 }); // true
```

The pattern suits a small, stable language that must be evaluated repeatedly, such as pricing rules, search filters, feature-flag conditions or permission policies. A typical trigger is a config format that grows by accident: a JSON filter gains `and`, then `or`, then nested groups, and the evaluation code becomes a tangle of special cases. Naming the grammar turns that into a defined set of node types. The resulting tree is an instance of the [composite](./Composite%20pattern.md) pattern.

The pattern describes evaluation and does not cover parsing. Text such as `age > 18 AND score > 700` still needs a parser to produce the tree, and that parser is often the larger piece of work.

Costs rise with the size of the grammar. One class per rule becomes hard to maintain for a large language, and walking a tree is slower than running compiled code. For anything substantial, use a parser generator or an existing language such as SQL or an embedded scripting engine. For combining business rules in code, the [specification pattern](./Specification%20pattern.md) is a narrower option built on the same idea.

Do not implement this by passing user input to `eval`, which gives that input access to the entire runtime. A dedicated interpreter can only do what its node types allow. Limit expression depth and size as well, so a crafted rule cannot exhaust CPU or the stack.

When many operations are needed on the tree, a [visitor](./Visitor%20pattern.md) keeps them out of the node classes.

_Usage:_

"Our discount rules JSON has grown nested `or` blocks and nobody can tell how they evaluate."

"It's a language now. Define the node types and write a small interpreter instead of more special cases."
