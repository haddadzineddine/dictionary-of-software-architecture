---
description: Representing a request as an object so it can be queued, logged, retried or undone.
---

The command pattern represents a request as an object that contains everything needed to carry it out. It is a behavioural pattern from the Gang of Four book (1994). The code that triggers an action, the invoker, holds a command and calls `execute()` without knowing what the action does or which object, the receiver, performs it.

```typescript
interface Command {
  execute(): void;
  undo(): void;
}

class RenameLayer implements Command {
  private previous = "";
  constructor(private layer: Layer, private name: string) {}

  execute() {
    this.previous = this.layer.name;
    this.layer.name = this.name;
  }

  undo() {
    this.layer.name = this.previous;
  }
}

class History {
  private done: Command[] = [];
  run(command: Command) {
    command.execute();
    this.done.push(command);
  }
  undo() {
    this.done.pop()?.undo();
  }
}
```

Turning a call into data allows things a direct method call cannot do:

| Capability      | How the command object enables it                   |
| --------------- | --------------------------------------------------- |
| Undo and redo   | Keep a history and call `undo()`                    |
| Queueing        | Store commands and run them later                   |
| Retry           | Run the same command again                          |
| Audit log       | Record each command with who issued it              |
| Shared triggers | A menu item, shortcut and button invoke one command |

A common motivation is undo added late. When UI handlers mutate state directly, there is no record of what happened, and undo requires rewriting every handler. Routing changes through commands gives each one a place to define its inverse.

Commands that cross a process boundary need care. A job queue typically delivers at least once, so a `ChargeCustomer` command can run twice and bill a customer twice unless it is idempotent. Serialise commands as plain data with an ID, since object references do not survive a queue.

Inverse operations can be difficult to write. Deleting a record may cascade, and sending an email cannot be reversed. For those steps, capture a snapshot with a [memento](./Memento%20pattern.md) or mark the command as not undoable.

A command differs from a [strategy](./Strategy%20pattern.md). A strategy supplies a way of doing a job the context already owns. A command represents a specific action, with its arguments, to be done at some point. The word "command" in [command-query separation](./Command-query%20separation.md) and CQRS is related, but it refers to an operation that changes state rather than this object structure.

Avoid the pattern when an action is only ever invoked directly. A plain function is enough.

_Usage:_

"Undo only works for about half of the editor's actions."

"The rest mutate state in their click handlers. Move them to commands with an `undo` method."
