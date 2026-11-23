---
description: An interface for creating families of related objects so code gets a matching set without naming concrete classes.
---

The abstract factory pattern provides an interface for creating a family of related objects without naming their concrete classes. It appears in the Gang of Four book (1994). Client code receives one factory and asks it for each product, so every product it gets belongs to the same family.

```typescript
interface CloudFactory {
  createStorage(): BlobStorage;
  createQueue(): MessageQueue;
}

class AwsFactory implements CloudFactory {
  createStorage() {
    return new S3Storage();
  }
  createQueue() {
    return new SqsQueue();
  }
}

class LocalFactory implements CloudFactory {
  createStorage() {
    return new DiskStorage();
  }
  createQueue() {
    return new InMemoryQueue();
  }
}

function startApp(cloud: CloudFactory) {
  const storage = cloud.createStorage();
  const queue = cloud.createQueue();
  // ...
}
```

The pattern prevents mismatched combinations. Without it, each piece is selected independently, often by separate environment checks. A staging deploy can then write files to local disk while publishing jobs to a real queue, and workers fail because the file they were told to process is not there. With a single factory, the environment is chosen once, at startup, and the choice applies to every product.

Adding a family and adding a product have different costs:

| Change                               | Effort                                       |
| ------------------------------------ | -------------------------------------------- |
| Add a family (for example, GCP)      | Add one factory class; clients are unchanged |
| Add a product (for example, a cache) | Change the interface and every factory       |

Choose the pattern when families change more often than the product list. If products vary independently, so any storage can pair with any queue, the family constraint is false and separate configuration is clearer.

The pattern differs from [factory method](./Factory%20method.md) in scope. A factory method creates one product, usually through a subclass hook. An abstract factory is a separate object with several creation methods, usually passed to clients through dependency injection. Implementations of an abstract factory often use factory methods internally.

Avoid it when there is only one family. A `CloudFactory` with a single `AwsFactory` implementation is [premature abstraction](./Premature%20abstraction.md), and every new product must then be threaded through an interface that offers no choice.

_Usage:_

"Staging wrote to the local disk but queued jobs on real SQS."

"Those were picked by separate flags. Use one environment factory so they can't diverge."
