# Software Architecture and Design Patterns Dictionary

A plain-English dictionary of how software is structured: design principles, coupling and modularity, object-oriented design patterns, enterprise application patterns, domain modelling, architecture styles, architecture practice and anti-patterns.

Why does a one-line change touch twelve files? Why can't this class be tested without a database? Why did splitting the app into services make deploys slower?

Each of these has a short explanation once you know the right words. Entries define the term, describe the failure it explains where there is one, and end with a short example of engineers using it.

Some architecture patterns are defined in companion dictionaries. [System Design](https://github.com/haddadzineddine/dictionary-of-system-design) covers monoliths, microservices, CQRS, sagas, event sourcing, the outbox pattern, the strangler fig, circuit breakers, bulkheads, backends for frontends and non-functional requirements. [Backend Engineering](https://github.com/haddadzineddine/dictionary-of-backend-engineering) covers layered architecture, hexagonal architecture, domain-driven design, bounded contexts, dependency injection and the repository pattern.

---

## Table of contents

- **[Section 1 — Design Principles](#section-1--design-principles)**
  - [SOLID](#solid)
  - [Single responsibility principle](#single-responsibility-principle)
  - [Open-closed principle](#open-closed-principle)
  - [Liskov substitution principle](#liskov-substitution-principle)
  - [Interface segregation principle](#interface-segregation-principle)
  - [Dependency inversion principle](#dependency-inversion-principle)
  - [DRY](#dry)
  - [KISS](#kiss)
  - [YAGNI](#yagni)
  - [Separation of concerns](#separation-of-concerns)
  - [Composition over inheritance](#composition-over-inheritance)
  - [Law of Demeter](#law-of-demeter)
  - [Tell don't ask](#tell-dont-ask)
  - [Command-query separation](#command-query-separation)
  - [Principle of least astonishment](#principle-of-least-astonishment)
  - [Encapsulation](#encapsulation)
  - [Information hiding](#information-hiding)
- **[Section 2 — Coupling and Modularity](#section-2--coupling-and-modularity)**
  - [Coupling](#coupling)
  - [Cohesion](#cohesion)
  - [Connascence](#connascence)
  - [Abstraction](#abstraction)
  - [Leaky abstraction](#leaky-abstraction)
  - [Deep module](#deep-module)
  - [Seam](#seam)
  - [Inversion of control](#inversion-of-control)
  - [Service locator](#service-locator)
  - [Circular dependency](#circular-dependency)
  - [Stable dependencies principle](#stable-dependencies-principle)
  - [Acyclic dependencies principle](#acyclic-dependencies-principle)
  - [Package by feature](#package-by-feature)
- **[Section 3 — Creational Patterns](#section-3--creational-patterns)**
  - [Factory method](#factory-method)
  - [Abstract factory](#abstract-factory)
  - [Builder pattern](#builder-pattern)
  - [Prototype pattern](#prototype-pattern)
  - [Singleton](#singleton)
  - [Object pool](#object-pool)
- **[Section 4 — Structural Patterns](#section-4--structural-patterns)**
  - [Adapter pattern](#adapter-pattern)
  - [Bridge pattern](#bridge-pattern)
  - [Composite pattern](#composite-pattern)
  - [Decorator pattern](#decorator-pattern)
  - [Facade pattern](#facade-pattern)
  - [Flyweight pattern](#flyweight-pattern)
  - [Proxy pattern](#proxy-pattern)
- **[Section 5 — Behavioral Patterns](#section-5--behavioral-patterns)**
  - [Chain of responsibility](#chain-of-responsibility)
  - [Command pattern](#command-pattern)
  - [Interpreter pattern](#interpreter-pattern)
  - [Iterator pattern](#iterator-pattern)
  - [Mediator pattern](#mediator-pattern)
  - [Memento pattern](#memento-pattern)
  - [Observer pattern](#observer-pattern)
  - [State pattern](#state-pattern)
  - [Strategy pattern](#strategy-pattern)
  - [Template method](#template-method)
  - [Visitor pattern](#visitor-pattern)
  - [Null object pattern](#null-object-pattern)
- **[Section 6 — Enterprise Application Patterns](#section-6--enterprise-application-patterns)**
  - [Transaction script](#transaction-script)
  - [Domain model](#domain-model)
  - [Service layer](#service-layer)
  - [Active record](#active-record)
  - [Data mapper](#data-mapper)
  - [Unit of work](#unit-of-work)
  - [Identity map](#identity-map)
  - [Lazy load](#lazy-load)
  - [Data transfer object](#data-transfer-object)
  - [Gateway pattern](#gateway-pattern)
  - [Specification pattern](#specification-pattern)
  - [Plugin architecture](#plugin-architecture)
  - [Front controller](#front-controller)
  - [Model-view-controller](#model-view-controller)
  - [Model-view-presenter](#model-view-presenter)
  - [Model-view-viewmodel](#model-view-viewmodel)
- **[Section 7 — Domain Modelling](#section-7--domain-modelling)**
  - [Ubiquitous language](#ubiquitous-language)
  - [Context map](#context-map)
  - [Subdomain](#subdomain)
  - [Core domain](#core-domain)
  - [Shared kernel](#shared-kernel)
  - [Anti-corruption layer](#anti-corruption-layer)
  - [Entity](#entity)
  - [Value object](#value-object)
  - [Aggregate](#aggregate)
  - [Domain event](#domain-event)
  - [Domain service](#domain-service)
  - [Invariant](#invariant)
  - [Event storming](#event-storming)
- **[Section 8 — Architecture Styles](#section-8--architecture-styles)**
  - [Clean architecture](#clean-architecture)
  - [Onion architecture](#onion-architecture)
  - [Vertical slice architecture](#vertical-slice-architecture)
  - [Pipes and filters](#pipes-and-filters)
  - [Microkernel architecture](#microkernel-architecture)
  - [Service-oriented architecture](#service-oriented-architecture)
  - [Space-based architecture](#space-based-architecture)
  - [Blackboard pattern](#blackboard-pattern)
  - [Client-server architecture](#client-server-architecture)
  - [Peer-to-peer architecture](#peer-to-peer-architecture)
  - [Cell-based architecture](#cell-based-architecture)
- **[Section 9 — Architecture Practice](#section-9--architecture-practice)**
  - [Software architecture](#software-architecture)
  - [Architecture decision record](#architecture-decision-record)
  - [Quality attribute](#quality-attribute)
  - [Architectural trade-off](#architectural-trade-off)
  - [Fitness function](#fitness-function)
  - [Evolutionary architecture](#evolutionary-architecture)
  - [C4 model](#c4-model)
  - [Architecture Tradeoff Analysis Method](#architecture-tradeoff-analysis-method)
  - [Conway's law](#conways-law)
  - [Inverse Conway maneuver](#inverse-conway-maneuver)
  - [Team Topologies](#team-topologies)
  - [Walking skeleton](#walking-skeleton)
  - [Architectural drift](#architectural-drift)
  - [Technical debt](#technical-debt)
  - [Reference architecture](#reference-architecture)
  - [Last responsible moment](#last-responsible-moment)
- **[Section 10 — Anti-Patterns](#section-10--anti-patterns)**
  - [Anti-pattern](#anti-pattern)
  - [Big ball of mud](#big-ball-of-mud)
  - [God object](#god-object)
  - [Anemic domain model](#anemic-domain-model)
  - [Distributed monolith](#distributed-monolith)
  - [Spaghetti code](#spaghetti-code)
  - [Lava flow](#lava-flow)
  - [Golden hammer](#golden-hammer)
  - [Shotgun surgery](#shotgun-surgery)
  - [Feature envy](#feature-envy)
  - [Primitive obsession](#primitive-obsession)
  - [Speculative generality](#speculative-generality)
  - [Cargo cult programming](#cargo-cult-programming)
  - [Premature abstraction](#premature-abstraction)
  - [Inner-platform effect](#inner-platform-effect)
  - [Not invented here](#not-invented-here)

## Section 1 — Design Principles

### SOLID

SOLID is an acronym for five object-oriented design principles that aim to keep code changeable as it grows. Robert C. Martin gathered the principles, and Michael Feathers proposed the acronym.

| Letter | Principle                                                              | Rule                                               | Violation looks like                         |
| ------ | ---------------------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| S      | [Single responsibility](#single-responsibility-principle)      | A module answers to one group of stakeholders      | A billing change breaks a report             |
| O      | [Open-closed](#open-closed-principle)                            | Add behaviour without editing stable code          | Each payment type edits the same `switch`    |
| L      | [Liskov substitution](#liskov-substitution-principle)          | Subtypes honour the parent's contract              | A subclass throws on an inherited method     |
| I      | [Interface segregation](#interface-segregation-principle)      | Clients depend only on the methods they use        | A test mocks twenty methods to use two       |
| D      | [Dependency inversion](#dependency-inversion-principle)        | Policy depends on [abstractions](#abstraction) | Business rules import the database driver    |

The principles address a common experience: a small feature request touches many unrelated files, and a fix in one place breaks something elsewhere. Each principle targets one source of that [coupling](#coupling), such as a class with too many jobs, a subclass that breaks its parent's contract, or a dependency that points toward a volatile detail.

The principles are heuristics, and applying them mechanically causes a different problem. An interface for every class, a file for every method and several layers of forwarding make a simple flow hard to follow. That outcome is a form of [premature abstraction](#premature-abstraction). Apply a principle when the code shows the pressure it relieves. Two payment types do not need a plugin system, while a fifth might justify one. [YAGNI](#yagni) and [KISS](#kiss) act as counterweights.

SOLID was written with classes in mind, but most of it carries over to functions and modules in TypeScript. A function type can act as an interface, and a module boundary can hold a single responsibility. Substitution applies to anything with a contract, including an HTTP API whose new version must keep accepting old requests.

_Usage:_

"Should this new class get an interface so it follows SOLID?"

"Only if there's a second implementation or a test that needs one. Otherwise it's an extra file with no benefit."

### Single responsibility principle

The single responsibility principle says a module should have one reason to change. Robert C. Martin, who named it as part of [SOLID](#solid), later restated it as a module being responsible to one actor, meaning one group of stakeholders who request changes.

The principle is often misread as "a class should do one thing", which leads to many tiny classes. The actual test concerns who drives change. A class can have several methods and still satisfy the principle if one group's needs determine all of them.

The symptom is a change for one team breaking behaviour for another. Finance asks for a new overtime calculation, a developer edits the shared `regularHours()` helper, and an HR report that relied on the old figure changes without anyone noticing. Both groups' requirements meet in the same code, so unrelated work also produces merge conflicts.

```typescript
// Three actors, one class
class Employee {
  calculatePay() {} // finance
  reportHours() {} // HR
  save() {} // platform team
}
```

The usual fix is to split by actor into `PayCalculator`, `HoursReporter` and `EmployeeStore`, each working on shared employee data. A [facade](#facade-pattern) can keep one entry point for callers that want it.

Splitting has a cost. Code that always changes together belongs together, and separating it creates [shotgun surgery](#shotgun-surgery), where one change touches many files. Aim for high [cohesion](#cohesion): group what changes for the same reason and separate what changes for different reasons. At the other extreme, a class that keeps accumulating responsibilities becomes a [god object](#god-object).

Apply the principle when you see the pressure, such as two teams repeatedly editing one file. A small class with a single user does not need splitting because it could one day have two.

_Usage:_

"Why did the payroll fix change the numbers on the HR dashboard?"

"Both use the same hours method on `Employee`. That's two reasons to change in one class, so let's split it."

### Open-closed principle

The open-closed principle says a module should be open for extension and closed for modification, so that new behaviour can be added without editing code that already works. Bertrand Meyer stated it in _Object-Oriented Software Construction_ (1988), using inheritance. Robert C. Martin later reframed it around interfaces and polymorphism, and it became the O in [SOLID](#solid).

The symptom is a `switch` that every new feature has to edit. Adding a payment method means changing the checkout function, the refund function and the receipt function, and each edit risks breaking the methods that already work.

```typescript
interface PaymentMethod {
  charge(amount: Money): Promise<Receipt>;
  refund(receipt: Receipt): Promise<void>;
}

// A new provider is a new class. checkout() does not change.
async function checkout(method: PaymentMethod, amount: Money) {
  return method.charge(amount);
}
```

The variation now sits behind an interface, usually through the [strategy pattern](#strategy-pattern) or a [plugin architecture](#plugin-architecture). The calling code stays closed, and each new variant is a new module.

No design is closed against every kind of change. The interface above makes adding a payment method cheap, but adding an operation such as `authorize` requires editing every implementation. A `switch` has the reverse trade-off: a new operation is one new function, while a new variant touches all of them. Choose based on which of the two actually changes in your system.

Avoid building extension points in advance. Guessing at future variation produces [speculative generality](#speculative-generality), and the guess is often wrong. Write the direct version first, then introduce an [abstraction](#abstraction) when a second or third variant shows what really differs. For a closed set of cases that rarely changes, such as days of the week, a `switch` with exhaustive type checking is simpler.

_Usage:_

"Every new payment provider means editing five `switch` statements."

"We have four providers and more coming. Let's move them behind a `PaymentMethod` interface."

### Liskov substitution principle

The Liskov substitution principle says that code written against a type must keep working when given any of its subtypes. Barbara Liskov introduced the idea in a 1987 keynote, and she and Jeannette Wing formalised it in a 1994 paper. It is the L in [SOLID](#solid).

The compiler checks method signatures but not behaviour, so a subtype can type-check and still break its callers. The symptom is an `instanceof` check added to a caller because one subclass behaves differently, or a method that throws `NotImplementedError` in one subclass.

```typescript
class Rectangle {
  constructor(public width: number, public height: number) {}
  setWidth(w: number) { this.width = w; }
  area() { return this.width * this.height; }
}

class Square extends Rectangle {
  setWidth(w: number) { this.width = w; this.height = w; }
}

// With a height of 4, a Rectangle returns 20. A Square returns 25.
function stretch(r: Rectangle) {
  r.setWidth(5);
  return r.area();
}
```

A subtype must honour the contract of its parent:

| Rule                         | Meaning                           | Violation                                  |
| ---------------------------- | --------------------------------- | ------------------------------------------ |
| Preconditions                | Cannot demand more from callers   | Rejects input the parent accepts           |
| Postconditions               | Cannot promise less               | Returns `null` where the parent never does |
| [Invariants](#invariant) | Must preserve what is always true | `Square` ties width to height              |
| Exceptions                   | Cannot add new kinds of failure   | `ReadOnlyList.add()` throws                |

The fix is usually to remove the inheritance relationship. "Is a" in everyday language does not imply substitutability: a square is a rectangle in geometry, but it is not a mutable `Rectangle` object. Use a narrower shared interface such as `Shape { area(): number }`, or apply [composition over inheritance](#composition-over-inheritance).

The principle applies beyond classes. A new version of an API, a replacement storage driver and a fake used in tests are all substitutes, and each must honour what callers rely on.

_Usage:_

"Why is there an `instanceof ReadOnlyCache` check in the save path?"

"Its `set` throws, so it can't stand in for `Cache`. Give it a read-only interface and stop inheriting."

### Interface segregation principle

The interface segregation principle says that no client should be forced to depend on methods it does not use. Instead of one large interface, define smaller ones shaped around what each caller needs. It is the I in [SOLID](#solid), formulated by Robert C. Martin.

The symptom is a test that stubs twenty methods so a function can call two of them, or a change to an unrelated method that forces a rebuild of code that never calls it. Implementers are affected too. A class may have to write `throw new Error("not supported")` for methods that make no sense for it, which also breaks the [Liskov substitution principle](#liskov-substitution-principle).

```typescript
interface UserStore {
  findById(id: string): Promise<User>;
  search(query: string): Promise<User[]>;
  save(user: User): Promise<void>;
  delete(id: string): Promise<void>;
  exportAll(): Promise<Buffer>;
}

// This consumer names only what it needs
type UserReader = Pick<UserStore, "findById">;

async function greeting(users: UserReader, id: string) {
  const user = await users.findById(id);
  return `Hello, ${user.name}`;
}
```

TypeScript makes this inexpensive because its types are structural. A function can declare a narrow parameter type with `Pick` or an inline interface, and any object with those methods satisfies it, with no change to the concrete class. A test can then pass a small object with one method.

Narrow interfaces reduce [coupling](#coupling) and document what a function actually uses. The principle differs from the [single responsibility principle](#single-responsibility-principle) in viewpoint: single responsibility concerns why an implementation changes, while segregation concerns what a caller can see. One class may legitimately implement several narrow interfaces.

Over-applied, the principle produces a one-method interface per call site and many near-identical types. Split where consumers genuinely differ. An interface that its callers use in full should stay whole, and a [deep module](#deep-module) with a small interface often avoids the problem from the start.

_Usage:_

"This test mocks the whole `UserStore` just to read one user."

"The function only calls `findById`. Narrow its parameter to that and the test needs a one-line stub."

### Dependency inversion principle

The dependency inversion principle says high-level modules should not depend on low-level modules, and that both should depend on [abstractions](#abstraction). It is the D in [SOLID](#solid), stated by Robert C. Martin. In practice, business rules define the interface they need, and infrastructure implements it.

The symptom is business logic that cannot run without its infrastructure. Testing a pricing rule requires a running database, or replacing an email vendor means editing the order code, because `OrderService` imports the vendor SDK directly.

```typescript
// orders/order-service.ts: the policy owns the interface
export interface Notifier {
  orderPlaced(order: Order): Promise<void>;
}

export class OrderService {
  constructor(private notifier: Notifier) {}

  async place(order: Order) {
    await this.notifier.orderPlaced(order);
  }
}

// infrastructure/email-notifier.ts: the detail depends on the policy
import type { Notifier } from "../orders/order-service";

export class EmailNotifier implements Notifier {
  async orderPlaced(order: Order) {
    /* call the vendor API */
  }
}
```

The inversion refers to the direction of the source-code dependency. Control still flows from `OrderService` to the email code at runtime, but the import arrow now points from infrastructure toward the business rules. The location of the interface matters: if it sits in the infrastructure package, the business code still depends on that package and nothing has been inverted.

Three related terms are often confused:

| Term                                                | What it is                                               |
| --------------------------------------------------- | -------------------------------------------------------- |
| Dependency inversion                                | A design rule about which way source dependencies point  |
| Dependency injection                                | A technique for passing a dependency in from outside     |
| [Inversion of control](#inversion-of-control) | A framework or caller decides when your code runs      |

This rule underpins [clean architecture](#clean-architecture), [onion architecture](#onion-architecture) and hexagonal architecture. It costs an interface and a wiring step at each boundary. Apply it where the detail is likely to change or is awkward to test, such as databases, payment gateways and third-party APIs. Wrapping a stable utility library or a pure function adds indirection with no benefit.

_Usage:_

"We can't test the discount logic without Postgres running."

"It imports the client directly. Have the service define a small interface and pass the Postgres version in at startup."

### DRY

DRY stands for "don't repeat yourself". Andy Hunt and Dave Thomas defined it in _The Pragmatic Programmer_ (1999): "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."

The principle concerns knowledge rather than text. A tax rate, a validation rule or the definition of an active customer should live in one place. When it is duplicated, the symptom is a fix applied in three places out of four: the checkout shows one price, the invoice shows another, and nobody knows which is correct. The scattered edits that follow are known as [shotgun surgery](#shotgun-surgery).

Code that looks the same is not always the same knowledge. Two functions may both check that a string is under 100 characters, one for a username and one for a product title. They match by coincidence and will change for different reasons. Merging them creates [coupling](#coupling) between unrelated features, and the shared helper gradually gains flags such as `isAdmin` or `skipValidation` as each caller's needs diverge.

| Duplication    | Example                                 | Action                |
| -------------- | --------------------------------------- | --------------------- |
| Same knowledge | Tax rate defined in two services        | Consolidate           |
| Coincidental   | Similar validation for unrelated fields | Leave it              |
| Unclear        | Two similar handlers                    | Wait for a third case |

The last row reflects a common rule of thumb called the rule of three: tolerate a second copy and extract on the third, when the shared shape is visible. Extracting sooner risks a [premature abstraction](#premature-abstraction). Undoing a wrong abstraction usually costs more than removing duplication, because every caller has to be untangled.

DRY has a further cost across service or team boundaries. A shared library used by several services means a change can require coordinated releases, which can produce a [distributed monolith](#distributed-monolith). Duplicating a small amount of code between independently deployed services is often the better trade-off.

_Usage:_

"These two handlers have the same ten lines. Should I extract a helper?"

"One's for refunds, one's for payouts, and finance keeps changing them separately. Leave them apart for now."

### KISS

KISS stands for "keep it simple, stupid", a guideline to choose the simplest design that meets the requirement. The phrase is commonly attributed to Lockheed engineer Kelly Johnson. In software, it means avoiding moving parts the problem does not require.

The symptom is a small task that takes days because of the structure around it. Adding a field to a form means editing a controller, a service, a mapper, two [data transfer objects](#data-transfer-object) and a factory, each of which only forwards the value. New team members need a diagram to follow a single request, and bugs appear in the handoffs between layers.

Complexity has a running cost. Everyone who reads, debugs or changes the code pays it, long after the person who added it has moved on. Simple code is easier to test, delete and replace.

Simple does not mean short. A clever one-liner can be harder to follow than five plain lines, and a single large script can be harder to maintain than two well-named modules. A useful test is how much a reader must hold in their head to make a correct change.

| Choice     | Simpler default         | Reach for more when                  |
| ---------- | ----------------------- | ------------------------------------ |
| Storage    | One relational database | A measured load or data shape needs it |
| Deployment | A single deployable     | Team or scaling needs diverge        |
| Variation  | An `if` statement       | Several variants keep growing        |
| Reuse      | A plain function        | Several callers share real knowledge |

KISS can be misused to reject necessary work. Error handling, input validation and security are required complexity, and removing them makes a system shorter but not simpler. Distinguish essential complexity, which comes from the problem, from accidental complexity, which comes from the solution. KISS targets the second. It is closely related to [YAGNI](#yagni), which is about not building for imagined future needs, whereas KISS concerns the shape of what you do build.

_Usage:_

"Do we need a queue and a worker for this nightly export?"

"It runs once a day and takes a minute. A cron job calling one function is enough."

### YAGNI

YAGNI stands for "you aren't gonna need it", a practice from Extreme Programming: do not build a capability until a current requirement calls for it.

The symptom is code that exists for a future that never arrived. A `StorageProvider` interface has one implementation, a config option has never been set to anything but its default, and a tenant column holds `1` in every row. Each of these still has to be read, tested and worked around, and later changes take longer because of them. The resulting smell is called [speculative generality](#speculative-generality).

A speculative feature costs more than the time to build it:

| Cost        | What happens                                                  |
| ----------- | ------------------------------------------------------------- |
| Build       | Time is taken from work with a known need                     |
| Delay       | Needed features ship later                                    |
| Carry       | Every later change must accommodate the extra code            |
| Wrong guess | The real need differs from the guess, so the code is reworked |

YAGNI depends on code being cheap to change later. Tests, clear module boundaries and regular refactoring are what make it safe to defer work. Without them, deferral turns into [technical debt](#technical-debt) rather than saved effort.

The practice applies to features and speculative flexibility, not to basic quality. Error handling, tests and readable names are part of building the current requirement. Some decisions are also expensive to reverse, such as public API shapes, data formats, identifiers and security models, and those justify more thought up front. The idea of the [last responsible moment](#last-responsible-moment) helps here: delay a decision until the cost of waiting exceeds the cost of deciding.

A practical check is to ask what it would cost to add the capability when it is needed. If the cost is about the same as now, wait. If it would require migrating every customer's data, decide now.

_Usage:_

"Should we make the notifier pluggable in case we add SMS?"

"Nobody has asked for SMS. Call the email service directly, and extract an interface if SMS actually comes up."

### Separation of concerns

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

Layered architecture separates on the technical axis, while [package by feature](#package-by-feature) separates on the business axis. Many systems use both, with features at the top level. Cross-cutting concerns often go in middleware or a [decorator](#decorator-pattern).

Separating the wrong things has a cost. Splitting code that always changes together spreads one change across many files, which reduces [cohesion](#cohesion). React components are a familiar example: combining markup and logic in one file was criticised at first as mixing concerns, but in many UIs the markup and its behaviour change together. A practical test for a boundary is whether you can change one side without reading the other.

_Usage:_

"The nightly job has its own copy of the discount logic."

"It's stuck inside the HTTP handler. Pull it out into a plain function and call it from both."

### Composition over inheritance

Composition over inheritance is the guideline to build behaviour by holding and delegating to other objects instead of extending a parent class. The Gang of Four book (1994) stated it as "favor object composition over class inheritance".

The symptom is a class hierarchy that multiplies. A `Notification` class gains `EmailNotification` and `SmsNotification`, then someone needs retries and urgency, producing `RetryingUrgentEmailNotification`. Changing a method in the base class can also break subclasses that relied on its internals, a problem known as the fragile base class.

```typescript
interface Channel {
  send(message: string): Promise<void>;
}

class Retrying implements Channel {
  constructor(private inner: Channel, private attempts: number) {}

  async send(message: string) {
    for (let i = 1; ; i++) {
      try {
        return await this.inner.send(message);
      } catch (error) {
        if (i >= this.attempts) throw error;
      }
    }
  }
}

const channel = new Retrying(new EmailChannel(), 3);
```

Each behaviour is now a small object, and combinations are assembled at runtime instead of declared as classes. The [decorator](#decorator-pattern) and [strategy](#strategy-pattern) patterns both work this way.

|                      | Inheritance                          | Composition                 |
| -------------------- | ------------------------------------ | --------------------------- |
| Relationship         | Is a                                 | Has a, uses a               |
| Binding              | Fixed at compile time                | Can change at runtime       |
| Access to internals  | Subclass sees protected state        | Only the public interface   |
| Combining behaviours | One parent, so combinations multiply | Any combination             |
| Boilerplate          | Methods inherited for free           | Forwarding may be needed    |

The guideline says "over", not "instead of". Inheritance fits when there is a true subtype relationship that satisfies the [Liskov substitution principle](#liskov-substitution-principle), the hierarchy is shallow, and the base class is designed to be extended, as in the [template method](#template-method) pattern. Composition has its own costs: more small objects, forwarding code, and behaviour spread across the wiring rather than visible in one class.

_Usage:_

"We need an urgent version of `RetryingEmailNotification`."

"That's a third level of subclass. Make retry and urgency wrappers around a `Channel` and combine them."

### Law of Demeter

The Law of Demeter is a guideline that a method should only talk to its immediate collaborators. It came from the Demeter project at Northeastern University in the late 1980s and is often summarised as "only talk to your friends". A method may call methods on itself, its parameters, objects it creates and its own fields.

The symptom is a chain of property accesses that reaches through several objects, often called a train wreck:

```typescript
// Reaches through customer, wallet and card
order.customer.wallet.primaryCard.charge(total);

// Tells the order what should happen
order.chargeCustomer(total);
```

The first line depends on the shape of four objects. When `wallet` becomes optional or customers get several payment methods, every caller with that chain breaks, and the fix spreads across the codebase as [shotgun surgery](#shotgun-surgery). Tests also suffer, because a mock has to return a mock that returns a mock.

Each reach adds [coupling](#coupling) to a structure the caller should not need to know about. Following the law moves behaviour to the object that owns the data, which is the same direction as [tell don't ask](#tell-dont-ask).

The law is not about counting dots:

| Code                                | Violation? | Why                                   |
| ----------------------------------- | ---------- | ------------------------------------- |
| `order.customer.wallet.primaryCard` | Yes        | Navigates another object's internals  |
| `items.filter(isPaid).map(toTotal)` | No         | Each call returns a new collection    |
| `query.where(a).orderBy(b)`         | No         | A fluent builder returns itself       |
| `dto.address.city`                  | Usually no | Plain data with no behaviour to hide  |

Applied rigidly, the law produces wrapper methods such as `order.getCustomerWalletCardLast4()` that only forward calls, and the outer class grows with every new need. If many such forwards accumulate, the data may be in the wrong place, or the caller may need a different object passed in directly. Passing `card` as a parameter is often simpler than adding a method to reach it.

_Usage:_

"Making `wallet` optional broke forty call sites."

"They all reach through `customer.wallet.primaryCard`. Put a method on `Customer` so the path lives in one place."

### Tell don't ask

Tell don't ask is the guideline that code should tell an object what to do, rather than asking for its state and making the decision outside it. Data and the rules that govern it stay in the same place.

The symptom is the same conditional appearing in several callers. The checkout, the admin panel and a background job each read `account.balance`, compare it to the amount and subtract. One of them forgets the overdraft rule, and accounts go negative.

```typescript
// Ask: the caller holds the rule
if (account.balance >= amount) {
  account.balance -= amount;
}

// Tell: the account holds the rule
account.withdraw(amount);

class Account {
  constructor(private balance: number) {}

  withdraw(amount: number) {
    if (amount > this.balance) throw new InsufficientFunds();
    this.balance -= amount;
  }
}
```

This protects an [invariant](#invariant), because the balance can only change through a method that checks it, and it strengthens [encapsulation](#encapsulation). Code that repeatedly pulls data out of another object to work on it shows [feature envy](#feature-envy). A model with only getters and setters, with all rules in services, is an [anemic domain model](#anemic-domain-model).

Reading state remains normal and necessary in many places:

| Situation                              | Approach                                            |
| -------------------------------------- | --------------------------------------------------- |
| A rule about the object's own data     | Tell                                                |
| Showing data on a screen or a response | Ask                                                 |
| A decision spanning several objects    | Use a [domain service](#domain-service)       |
| Reports and queries                    | Read directly                                       |

Following the rule everywhere creates its own problem. If an `Order` gains `renderHtml()` and `toCsv()` so that nobody has to ask for its fields, it accumulates presentation concerns and moves toward a [god object](#god-object). Keep business rules with the data, and let display code read what it needs.

Tell don't ask overlaps with the [Law of Demeter](#law-of-demeter), since both reduce how much callers know about another object's internals. Demeter limits which objects a method can talk to, while this guideline concerns where a decision lives.

_Usage:_

"Support found accounts with negative balances."

"Three places check the balance and subtract on their own. Move it into `account.withdraw()` so the rule exists once."

### Command-query separation

Command-query separation is the rule that a method should either be a command, which changes state and returns nothing, or a query, which returns data and changes nothing. Bertrand Meyer defined it in his work on the Eiffel language and in _Object-Oriented Software Construction_.

The symptom is a bug caused by a call that looks like a read. A developer adds a `getUser()` call to a log statement and the system starts misbehaving, because `getUser()` also creates the user if missing or increments a login counter. Logging, retrying or reordering the call now changes behaviour.

```typescript
// Mixed: looks like a read, but writes
function getNextInvoiceNumber(): number {
  return ++counter;
}

// Separated
function currentInvoiceNumber(): number {
  return counter;
}

function advanceInvoiceNumber(): void {
  counter += 1;
}
```

Queries that follow the rule are safe to call repeatedly, cache, log and reorder, so a reader can reason about them without tracing into their bodies. A getter with a hidden write breaks the [principle of least astonishment](#principle-of-least-astonishment). Commands fit [tell don't ask](#tell-dont-ask), where callers instruct an object and do not inspect its state first.

There are legitimate exceptions, mostly where a read and a write must happen atomically:

| Operation                   | Why it mixes both                             |
| --------------------------- | --------------------------------------------- |
| `stack.pop()`               | Removes and returns in one step               |
| `INSERT ... RETURNING id`   | The caller needs the generated key            |
| `counter.incrementAndGet()` | Separate calls would race                     |
| Compare-and-swap            | The check and the write must be one operation |

The invoice example above shows the risk. With concurrent callers, two requests can read the same number before either advances it, so a real invoice counter needs one atomic operation. Follow the rule by default, and when it must be broken, name the method so the side effect is visible, such as `claimNextInvoiceNumber()`.

Command-query separation is different from CQRS. This rule applies to a single method or object. CQRS applies the same split at the architectural level, with separate models, and sometimes separate data stores, for reads and writes. A codebase can follow one without the other.

_Usage:_

"Adding a debug log changed the test results."

"The log calls `getSession()`, and that refreshes the expiry. Split it into a read and an explicit `refreshSession()`."

### Principle of least astonishment

The principle of least astonishment says a component should behave in the way most of its users expect. It applies to API design, naming, defaults, configuration and user interfaces. When behaviour and expectation differ, the design is usually the thing to change.

The symptom is a bug caused by a reasonable assumption. JavaScript's `sort()` compares values as strings by default, so `[10, 9, 1].sort()` returns `[1, 10, 9]`. Application code produces the same kind of surprise:

| Surprise                                 | Expectation                    | Fix                       |
| ---------------------------------------- | ------------------------------ | ------------------------- |
| `delete()` only archives                 | The record is gone             | Name it `archive()`       |
| `getUser()` writes to the database       | Reads have no effects          | Separate the write        |
| The default is to retry forever          | Calls eventually fail          | Use a bounded default     |
| One parser throws, another returns `null` | Errors work the same way      | Pick one convention       |
| A CLI flag deletes without confirmation  | Destructive actions ask first  | Require explicit consent  |

Expectation depends on the audience. The conventions of the language, framework and codebase set what users assume, so an API should follow them even where a different design might be slightly better in isolation. A method named `map` should behave like `map` everywhere else in that language.

Surprises cost the most at boundaries that are hard to change, such as a public API, a CLI or a library. After release, callers come to depend on the surprising behaviour, so correcting it becomes a breaking change. Review names and defaults before publishing them.

Apply the principle by making side effects visible in names, choosing safe defaults and staying consistent with neighbouring code. [Command-query separation](#command-query-separation) removes one common source of surprise, and a shared [ubiquitous language](#ubiquitous-language) reduces another by keeping names aligned with what the business means. Where unusual behaviour is necessary, document it at the point of use.

_Usage:_

"I called `user.delete()` and the row is still there."

"It soft-deletes. That surprises everyone, so let's rename it `archive()` before more code depends on it."

### Encapsulation

Encapsulation is the bundling of data with the operations that act on it, along with restricting direct outside access to that data. In TypeScript this usually means a class with private fields and public methods, or a module that exports functions but not its internal state. The object controls how its data changes, so it can guarantee an [invariant](#invariant).

The symptom of weak encapsulation is a value in an impossible state with no obvious culprit. An order has a negative total, or a `shipped` status with no shipping address, and finding the cause means searching every place that assigns to those fields, because any code can write to them.

```typescript
class Order {
  #items: LineItem[] = [];
  #status: "draft" | "placed" = "draft";

  addItem(item: LineItem) {
    if (this.#status !== "draft") throw new Error("Order is already placed");
    this.#items.push(item);
  }

  get items(): readonly LineItem[] {
    return this.#items;
  }
}
```

Private keywords alone do not achieve encapsulation. A private field with a public getter and setter offers the same access as a public field. Returning a mutable internal array lets callers change it from outside, which is why the getter above returns a `readonly` type. TypeScript's `private` is removed at compile time, while `#` fields are enforced at runtime.

Encapsulation is often conflated with [information hiding](#information-hiding). Encapsulation is a language mechanism for grouping and restricting access. Information hiding is a design decision about which details other modules should not depend on. A class can be fully encapsulated and still expose its design through a method such as `getMySqlConnection()`.

Not all data needs encapsulating. A [data transfer object](#data-transfer-object) or a plain configuration record has no rules to protect, and wrapping it in accessors adds code without adding safety. Apply encapsulation where there are rules about how data may change. Domain objects that hold such rules outside themselves form an [anemic domain model](#anemic-domain-model).

_Usage:_

"How did this order get shipped with no address?"

"Four services set `status` directly. Make it private and add a `ship()` method that checks the address."

### Information hiding

Information hiding is the design practice of giving each module a decision that is likely to change and concealing that decision from all other modules. David Parnas introduced it in his 1972 paper "On the Criteria To Be Used in Decomposing Systems into Modules". He argued that modules should be divided by what they hide, rather than by the steps in a processing flow.

The symptom of missing information hiding is a small technical change that spreads widely. Switching the date format, the cache key scheme or a database column means editing dozens of files, because each one learned the detail. When a storage change requires edits in the UI, the storage decision was not hidden.

The details worth hiding are those likely to change:

| Decision                    | Hidden behind                            |
| --------------------------- | ---------------------------------------- |
| Storage engine and schema   | A data access module                     |
| Third-party vendor          | An [adapter](#adapter-pattern)     |
| Algorithm                   | A function or [strategy](#strategy-pattern) |
| Data format on disk or wire | A serializer                             |
| Concurrency and caching     | A module's internal implementation       |

```typescript
// Leaks the decision: callers build the key
cache.get(`user:v2:${tenantId}:${userId}`);

// Hides it: the key format can change in one place
userCache.get(tenantId, userId);
```

Information hiding differs from [encapsulation](#encapsulation). Encapsulation is the language-level mechanism of restricting access, such as private fields. Information hiding is the design choice of what to conceal. A class can have only private fields and still leak a decision through a method like `getRedisKey()`, or through a return type that exposes a vendor's objects.

Hiding reduces [coupling](#coupling) and allows modules to be understood and changed independently. It is what makes a [deep module](#deep-module) possible: a small interface in front of a lot of hidden behaviour. No interface hides everything, because some details show through as latency, failures or ordering, which is the problem described by [leaky abstraction](#leaky-abstraction). Hiding also requires predicting what will change, so revise boundaries as actual changes show where the pressure is.

_Usage:_

"Why did renaming a cache key touch thirty files?"

"Every caller builds the key itself. Hide the format inside a `userCache` module."

## Section 2 — Coupling and Modularity

### Coupling

Coupling is the degree to which one module depends on another. Two modules are tightly coupled when a change in one is likely to require a change in the other, and loosely coupled when each can change independently. Larry Constantine developed the concept, and it was published with Edward Yourdon in _Structured Design_.

The symptom is a small change that spreads. Renaming a field breaks three services, one team's release waits on another team's, or a test fails in a module nobody touched.

The structured design scale lists these forms, from loosest to tightest:

| Form     | One module depends on                 | Example                         |
| -------- | ------------------------------------- | ------------------------------- |
| Data     | Only the values passed as parameters  | `tax(amount, rate)`             |
| Stamp    | A structure, using only part of it    | `tax(order)` reads one field    |
| Control  | A flag that steers the other's logic  | `render(data, isAdmin)`         |
| External | A shared format or protocol           | Two services parse the same file |
| Common   | Shared mutable global state           | A global `config` both modify   |
| Content  | Another module's internals            | Reading a private field         |

Coupling also exists outside the code. Temporal coupling means one service must be running for another to work. Deployment coupling means two components must be released together. A system split into services that must deploy together is a [distributed monolith](#distributed-monolith), which keeps the coupling of a monolith and adds network failure.

Some coupling is required, because modules that share nothing cannot cooperate. The goal is to make it deliberate: depend on a narrow, stable interface rather than on internals, and keep things that change together in the same module, which raises [cohesion](#cohesion). Techniques include [information hiding](#information-hiding) and the [dependency inversion principle](#dependency-inversion-principle). [Connascence](#connascence) gives a finer vocabulary for describing how two pieces of code are linked.

Removing coupling can go too far. Replacing a direct function call with an event bus hides the dependency without removing it and makes the flow harder to trace.

_Usage:_

"Why does a change to the user table need a release from the billing team?"

"Billing reads that table directly. They're coupled to our schema, so give them an API instead."

### Cohesion

Cohesion is the degree to which the elements inside a module belong together. A highly cohesive module has one clear purpose, and its parts change for the same reasons. Like [coupling](#coupling), the term comes from Larry Constantine's structured design work. The two are usually discussed together, since modular design aims for high cohesion within modules and low coupling between them.

The symptom of low cohesion is a module you cannot describe without using "and", or a file named `utils.ts`, `helpers.ts` or `common.ts` that every other file imports. A change to one feature requires opening five folders, the files you open are mostly unrelated code, and unrelated work conflicts during merges.

The structured design scale ranks types of cohesion from weakest to strongest:

| Type            | Parts are grouped because       | Example                           |
| --------------- | ------------------------------- | --------------------------------- |
| Coincidental    | No real reason                  | `utils.ts`                        |
| Logical         | Same category of thing          | All validators in one file        |
| Temporal        | They run at the same time       | `startup()` does unrelated setup  |
| Procedural      | They run in sequence            | Steps in a long workflow function |
| Communicational | They use the same data          | Functions that all read a `Report` |
| Sequential      | One's output feeds the next     | Parse, then transform             |
| Functional      | They all contribute to one task | A `TaxCalculator`                 |

To raise cohesion, move code next to the code it changes with. [Package by feature](#package-by-feature) does this at the folder level, by placing a feature's routes, logic and queries together rather than scattering them across technical layers. At class level, the [single responsibility principle](#single-responsibility-principle) applies the same idea, and [feature envy](#feature-envy) is a sign that a method sits in the wrong class.

Cohesion and file size are separate matters. A 600-line module that does one thing may be more cohesive than six 100-line files that must be read together, and splitting it can make things worse. Ask whether a typical change stays within the module. If it does, the boundary is working.

_Usage:_

"`utils.ts` is 2,000 lines and everyone conflicts in it."

"Nothing in there is related. Move each helper next to the feature that uses it."

### Connascence

Connascence is a way of describing [coupling](#coupling) precisely: two pieces of code are connascent if changing one requires changing the other to keep the system correct. Meilir Page-Jones introduced the term in the 1990s. It names the kind of dependency, so a reviewer can say more than "these are too coupled".

The forms run from weaker to stronger:

| Form      | Visible | Both sides must agree on | Example                             |
| --------- | ------- | ------------------------ | ----------------------------------- |
| Name      | Static  | A name                   | A method name at a call site        |
| Type      | Static  | A type                   | A parameter type                    |
| Meaning   | Static  | What a value means       | `status === 3` means shipped        |
| Position  | Static  | An order                 | `createUser("Ada", true, false)`    |
| Algorithm | Static  | A computation            | Client and server hash the same way |
| Execution | Dynamic | The order of calls       | `connect()` before `send()`         |
| Timing    | Dynamic | When things happen       | A `sleep(100)` waiting for a job    |
| Value     | Dynamic | Related values           | Two copies of a price must match    |
| Identity  | Dynamic | The same instance        | Two modules must share one object   |

Static forms are visible in source code, while dynamic forms appear only at runtime and are harder to find. The symptom of a strong form is a bug with no compile error. Someone swaps two boolean arguments or changes what status `3` means, and the code still type-checks while behaving incorrectly.

```typescript
// Connascence of position
createUser("Ada", true, false);

// Connascence of name
createUser({ name: "Ada", isAdmin: true, sendInvite: false });
```

Three properties decide how much a given connascence matters: strength is how hard it is to detect and change, locality is how far apart the two pieces are, and degree is how many places are involved.

The practical guidance is to refactor strong forms into weaker ones, such as replacing a magic number with a named constant, which converts connascence of meaning into connascence of name. Connascence of algorithm is often the duplication that [DRY](#dry) targets. Keep the strong forms that remain close together, which also raises [cohesion](#cohesion). Two functions in one file that rely on call order are acceptable, while the same reliance across two services is a risk.

_Usage:_

"Why did swapping those two booleans compile but break signup?"

"That's connascence of position. Use a named options object and the compiler will catch it."

### Abstraction

An abstraction is a simplified view of something that keeps the details a user needs and leaves out the rest. A file is an abstraction over disk blocks, an HTTP client is one over sockets, and a `sendInvoice()` function is one over the steps needed to send an invoice. It lets a programmer work with a concept without thinking about how it is implemented.

Abstraction and [information hiding](#information-hiding) are related but distinct. Abstraction concerns what a caller sees and thinks about. Information hiding concerns which design decisions are kept out of reach. A good interface does both.

Abstractions come in different forms:

| Form                 | Hides                     | Example                    |
| -------------------- | ------------------------- | -------------------------- |
| Function             | Steps of a computation    | `calculateTax(order)`      |
| Data type            | Representation            | `Money` instead of a float |
| Interface            | Which implementation runs | `PaymentGateway`           |
| Module               | Internal structure        | A `billing` package        |
| Protocol or platform | The machinery beneath     | SQL, HTTP, a filesystem    |

A useful abstraction reduces what the reader must know. A poor one adds a name without removing any detail, so the reader has to open it anyway. The symptom is a wrapper whose methods pass through to one call, or a helper such as `fetchData(url, true, false, "legacy")`, where each flag exists because a caller needed something different. A [deep module](#deep-module) is the favourable shape: a small interface over substantial behaviour.

Abstractions are usually more useful when drawn from several working examples, because the examples show what actually varies. Introduced too early, they encode a guess, which is [premature abstraction](#premature-abstraction), and later requirements get forced into the wrong shape. Keeping some duplication until the pattern is clear is often cheaper than untangling the wrong design, a trade-off discussed under [DRY](#dry).

No abstraction is complete. Details such as latency or failure can show through, as described under [leaky abstraction](#leaky-abstraction).

_Usage:_

"This `fetchData` helper has five boolean flags now."

"Each caller wanted something different. Inline it and see what the calls actually have in common."

### Leaky abstraction

A leaky [abstraction](#abstraction) is one whose hidden details affect the people using it, so they have to understand the layer underneath anyway. Joel Spolsky popularised the term in his 2002 essay "The Law of Leaky Abstractions", which argued that all non-trivial abstractions leak to some degree.

The symptom is code that works until it meets a condition the interface did not mention. An ORM using [lazy loading](#lazy-load) makes a list page look like ordinary object access, then the page takes eight seconds because each `order.customer` runs a query. A remote call looks like a local function until the network times out.

| Abstraction           | What it hides        | How it leaks                         |
| --------------------- | -------------------- | ------------------------------------ |
| ORM                   | SQL and query plans  | N+1 queries, missing indexes         |
| Remote procedure call | The network          | Timeouts, partial failure, retries   |
| Filesystem            | Disks and mounts     | Slow or failed writes on network drives |
| Garbage collection    | Memory management    | Pauses, leaks through held references |
| `async`/`await`       | Concurrency          | Interleaving between awaits          |
| Object storage folders | A flat key space    | A rename is a copy and a delete      |

Some leaks come from design choices and can be avoided. A data access method that returns a query builder, a service that throws `PrismaClientKnownRequestError`, or a domain type with a `_id` field passes an implementation detail to callers. Return domain types, translate errors at the boundary, and use an [adapter](#adapter-pattern) or [anti-corruption layer](#anti-corruption-layer) around external systems.

Other leaks cannot be removed, because latency, failure and resource limits come from the hardware and network. For those, make the cost visible in the interface: return a `Promise`, accept a timeout, and offer batch operations. Presenting a network call as a plain getter hides information callers need.

Teams should know one level below the abstractions they rely on, such as SQL for ORM users and TCP basics for anyone calling HTTP services. The abstraction saves time in normal operation, and that knowledge is needed when it fails.

_Usage:_

"The orders page got slow, but the code is just a loop over `order.customer`."

"That property runs a query each time. The ORM is leaking, so load customers in one batch."

### Deep module

A deep module is one whose interface is small compared with the functionality behind it. John Ousterhout uses the term in _A Philosophy of Software Design_, weighing what a module provides against the complexity of its interface. A shallow module is the opposite: its interface is nearly as complicated as its implementation.

Unix file I/O is Ousterhout's standard example. Five calls, `open`, `read`, `write`, `lseek` and `close`, hide file layout, caching, permissions and disk scheduling.

The symptom of shallow modules is a call stack of methods that each do very little. To trace one request you open a controller, a service, a manager and a helper, each forwarding arguments to the next. Every layer adds a name and a signature to learn while hiding almost nothing. Splitting code into many tiny classes and functions often makes this worse.

```typescript
// Shallow: callers must know the steps and their order
const conn = await pool.acquire();
const stmt = await conn.prepare(sql);
const rows = await stmt.execute(params);
await stmt.close();
pool.release(conn);

// Deep: pooling, preparation and cleanup are hidden
const result = await db.query(sql, params);
```

|                      | Shallow                      | Deep                       |
| -------------------- | ---------------------------- | -------------------------- |
| Interface            | Wide, mirrors the internals  | Narrow, describes the task |
| Caller must know     | Steps, order, edge cases     | What they want done        |
| Changes to internals | Often reach callers          | Stay inside                |
| Testing              | Many mocks of internal parts | Test through the interface |

Deep modules are built through [information hiding](#information-hiding). Pull complexity downward, so the module handles retries, defaults and edge cases rather than pushing them to every caller. Merging two shallow classes that always change together often produces one deeper class and raises [cohesion](#cohesion).

Depth has limits. A module that hides too much can stop callers doing what they need, so keep common cases simple and offer an optional lower-level path for rare ones. A large module with unrelated contents is a [god object](#god-object), because depth comes from one purpose with much behind it and not from size alone.

_Usage:_

"To send an email I have to build a transport, a template and a retry policy first."

"That module is shallow. Give it one `send(to, template, data)` and keep the rest inside."

### Seam

A seam is a place in a program where behaviour can be changed without editing the code at that place. Michael Feathers defined the term in _Working Effectively with Legacy Code_, where seams are the means of getting untested code under test. Each seam has an enabling point, the place where you decide which behaviour is used.

The problem a seam solves is code you cannot test without triggering its side effects. A function charges a real card, sends a real email or reads the system clock, so the only way to exercise it is to run it for real, and it goes unrefactored because nobody can check the result.

```typescript
// No seam: the client and the clock are fixed inside the function
async function renewSubscription(id: string) {
  const sub = await stripe.subscriptions.retrieve(id);
  if (sub.endsAt < Date.now()) await stripe.invoices.create({ subscription: id });
}

// Seam: the parameters are the enabling point
async function renewSubscription(id: string, billing: Billing, now: () => number) {
  const sub = await billing.getSubscription(id);
  if (sub.endsAt < now()) await billing.invoice(id);
}
```

Feathers describes three kinds:

| Seam          | Enabling point                  | TypeScript example                       |
| ------------- | ------------------------------- | ---------------------------------------- |
| Object        | Which object is passed in       | A constructor or function parameter      |
| Link          | What is resolved at load time   | `vi.mock("./billing")`                   |
| Preprocessing | Substitution before compilation | A bundler's `define` replacing a constant |

Object seams are generally preferable because they are explicit in the signature. Module mocks need no change to the code, but they depend on file paths and can break when files move.

Seams are also useful outside tests. A feature flag, an [adapter](#adapter-pattern) or a [strategy](#strategy-pattern) is a seam for switching behaviour, and a strangler fig migration relies on a seam where traffic can be redirected.

Introduce a seam where you need to vary behaviour, often at the boundary with an external system. Adding one around every function adds parameters and indirection without benefit. In legacy code, make the smallest change that creates a seam, add tests around the behaviour, and then refactor.

_Usage:_

"I can't test renewals without hitting Stripe."

"Add a seam. Pass the billing client in as a parameter and give the test a fake."

### Inversion of control

Inversion of control is a design in which a framework or other outside code decides when your code runs, instead of your code directing the program flow. A library is something you call, while a framework calls you. The idea is often summarised as the Hollywood principle: "don't call us, we'll call you".

```typescript
// Your code controls the flow
const input = readRequest();
const result = handle(input);
writeResponse(result);

// The framework controls the flow
app.get("/orders/:id", async (req, res) => {
  res.json(await findOrder(req.params.id));
});
```

In the second example, the server owns the loop, parses the request and handles errors, and your handler runs only when a matching route arrives. Event listeners, React components, test runners and lifecycle hooks work the same way.

The term covers several mechanisms:

| Mechanism                                       | What is inverted             | Example                          |
| ----------------------------------------------- | ---------------------------- | -------------------------------- |
| Callback or event                               | Who triggers the code        | `button.addEventListener`        |
| Framework lifecycle                             | Who owns the main loop       | React rendering a component      |
| [Template method](#template-method)       | Who controls the steps       | A base class calling hooks       |
| Dependency injection                            | Who creates dependencies     | A constructor receiving a client |
| [Plugin architecture](#plugin-architecture) | Who decides what gets loaded | A host loading extensions      |

Martin Fowler argued in 2004 that "inversion of control" was too general a label for containers that wire objects together, and proposed the name dependency injection for that case. The two are still often used interchangeably. Inversion of control is the broad idea, dependency injection is one application of it, and the [dependency inversion principle](#dependency-inversion-principle) is a separate rule about which way source-code dependencies point.

The benefit is reuse, since a framework solves the general flow and you write only the specific parts. The cost is a flow that is harder to trace. The symptom is a stack trace full of framework internals, or a handler that never runs and reports no error because a registration was missed, with no call site to search for. Where the order of steps matters to the business, as in a payment sequence, keep it in explicit code.

_Usage:_

"Where is this handler called from? I can't find a call site."

"There isn't one. The framework invokes it through the route registration, so start there."

### Service locator

A service locator is a central registry that code calls at runtime to obtain its dependencies. Instead of receiving a logger or a database client, a class asks for one with something like `locator.get("db")`. It solves the problem of reaching shared services from deep in a call stack without passing them through every layer, and it is one way to achieve [inversion of control](#inversion-of-control).

```typescript
const locator = new Map<string, unknown>();
locator.set("mailer", new SmtpMailer());

class InvoiceService {
  send(invoice: Invoice) {
    const mailer = locator.get("mailer") as Mailer;
    return mailer.deliver(invoice);
  }
}
```

The main criticism is that dependencies become invisible. The signature of `InvoiceService` shows no need for a mailer, so the failure appears at runtime: a test or new entry point crashes with "service not registered" because something deep in the call chain asked for a service nobody set up. Tests must configure shared state and can interfere with each other. Some authors, including Mark Seemann, classify it as an [anti-pattern](#anti-pattern) for application code.

It differs from dependency injection in how the dependency arrives:

|                       | Service locator          | Dependency injection    |
| --------------------- | ------------------------ | ----------------------- |
| How code gets it      | Asks for it              | Receives it             |
| Visible in signature  | No                       | Yes                     |
| Missing one is found  | When the line runs       | At startup or compile time |
| Test setup            | Register in a registry   | Pass a fake             |
| Wiring effort         | Low                      | Passing through layers  |

The pattern still has legitimate uses. Plugin hosts often cannot know every service at compile time, and legacy code may need a way to reach a dependency without changing hundreds of signatures. React context is a related, scoped form, where a component reads a value provided higher in the tree.

Prefer constructor or function parameters in new code. If a locator is necessary, restrict calls to the outermost layer, such as a request handler, and pass resolved objects inward. This stops the locator growing into a global access path and a source of hidden [coupling](#coupling).

_Usage:_

"This test crashes with 'mailer not registered', but the class doesn't mention a mailer."

"It pulls one from the service locator. Pass the mailer to the constructor so the dependency is visible."

### Circular dependency

A circular dependency exists when two or more modules depend on each other, directly or through a chain. For example, A imports B, B imports C, and C imports A. None of the modules in the cycle can be built, tested or understood alone.

In JavaScript and TypeScript, the symptom is often a runtime error that appears after an unrelated change: `Class extends value undefined is not a constructor`, `Cannot access 'X' before initialization`, or an imported value that is unexpectedly `undefined`. One module runs before the other has finished initialising, so reordering an import can make the bug appear or vanish.

```typescript
// user.ts
import { sendWelcome } from "./email";
export const DEFAULT_SENDER = "hello@example.com";
export const signUp = (to: string) => sendWelcome(to);

// email.ts
import { DEFAULT_SENDER } from "./user";
const sender = DEFAULT_SENDER.toLowerCase(); // Throws when user.ts loads first
export const sendWelcome = (to: string) => deliver(sender, to);
```

`import type` statements are erased at compile time, so type-only cycles do not fail at runtime, although they can still show a design problem.

Beyond load errors, a cycle is [coupling](#coupling) that prevents independent change. Modules in a cycle effectively form one module and must be released together. The [acyclic dependencies principle](#acyclic-dependencies-principle) states this rule at the package level.

| Fix                                  | When it applies                                    |
| ------------------------------------ | -------------------------------------------------- |
| Extract shared code to a third module | Both depend on the same constant or type          |
| Apply [dependency inversion](#dependency-inversion-principle) | A low-level module calls back into a high-level one |
| Publish an event                     | One module only needs to notify another            |
| Pass a value as a parameter          | A function needs one value from the other module   |
| Merge the modules                    | They are really one concept                        |

Detect cycles with tools such as `madge`, `dependency-cruiser` or the ESLint `import/no-cycle` rule, and run them in CI, where the check acts as a [fitness function](#fitness-function). Moving an import inside a function avoids the load-order error but leaves the dependency in place.

_Usage:_

"Tests crash with 'Class extends value undefined', but only when run alone."

"That's an import cycle between `order` and `customer`. Move the shared base class into its own module."

### Stable dependencies principle

The stable dependencies principle says a package should only depend on packages that are more stable than itself. Robert C. Martin defined it as one of his package design principles. "Stable" here means hard to change because many other packages depend on it. It does not mean unchanging.

The symptom is a small edit to a volatile package forcing a large rebuild and retest. A shared `common` package imports a feature package for one helper. Every change to that feature now rebuilds everything that uses `common`, and a minor UI tweak can hold up other teams' releases.

Martin measures this with an instability metric, `I = Ce / (Ca + Ce)`. Ca, or afferent [coupling](#coupling), counts the packages that depend on this one. Ce, or efferent coupling, counts the packages this one depends on. The result runs from 0, stable, to 1, unstable.

| Package        | Ca  | Ce  | I    | Role                                |
| -------------- | --- | --- | ---- | ----------------------------------- |
| `domain-types` | 8   | 0   | 0.00 | Many depend on it, so it changes rarely |
| `billing`      | 2   | 3   | 0.60 | Sits in the middle                  |
| `admin-ui`     | 0   | 5   | 1.00 | Free to change                      |

The rule requires I to decrease along each dependency arrow, as in `admin-ui` to `billing` to `domain-types`.

A stable package is hard to change, so it should not contain things that need frequent change. Martin's companion rule, the stable abstractions principle, says stable packages should be abstract, so they can be extended without being modified, in line with the [open-closed principle](#open-closed-principle). When a stable package needs something from a volatile one, apply the [dependency inversion principle](#dependency-inversion-principle): define an interface in the stable package and implement it in the volatile one.

The metric is a guide. It counts dependencies without weighing them, and a concrete date library can sit at I = 0 without problems because it rarely changes. Use the numbers to find a widely used package that depends on a fast-changing one.

_Usage:_

"Why does a copy change in the admin UI rebuild everything?"

"`common` imports from `admin-ui`. That arrow points at something less stable, so move the helper down."

### Acyclic dependencies principle

The acyclic dependencies principle says the dependency graph between packages must have no cycles. Robert C. Martin defined it among his package design principles. Following dependencies from any package should never lead back to where you started, which makes the graph a directed acyclic graph.

It addresses what Martin called the "morning after syndrome". A developer's code worked yesterday, but today it fails because someone changed a package it depends on. Teams respond by coordinating releases, and when packages depend on one another in a loop, none can be released without the others. A [circular dependency](#circular-dependency) turns those packages into one large unit for building, testing and versioning, even though they live in separate directories.

| Graph   | Build order                      | Effect of a change                 |
| ------- | -------------------------------- | ---------------------------------- |
| Acyclic | A clear order from the leaves up | Affects only dependents            |
| Cyclic  | No valid order                   | Affects every package in the cycle |

```text
Before:  billing -> orders -> customers -> billing

After:   billing -> orders -> customers -> billing-api
         billing -> billing-api
```

Two standard techniques break a cycle. The first is the [dependency inversion principle](#dependency-inversion-principle): one package depends on an interface, and the other implements it, as `billing` implements `billing-api` above. The second is to extract the code both packages use into a new package that they both depend on. If the packages are really one concept, merging them is also an option.

Cycles are easier to prevent than to remove. They usually arrive through one small convenience import during ordinary work, so enforce the rule with a dependency check in CI, which acts as a [fitness function](#fitness-function). Once several cycles have formed, separating them takes planned effort, and the codebase drifts toward a [big ball of mud](#big-ball-of-mud).

The principle pairs with the [stable dependencies principle](#stable-dependencies-principle), which governs the direction the arrows should point. Cycles inside a single package are a smaller concern because the package is released as a unit, though they can still cause load-order errors.

_Usage:_

"Why can't we release `orders` without also releasing `billing`?"

"They depend on each other through `customers`. Extract a `billing-api` package to break the cycle."

### Package by feature

Package by feature is a way of organising source code so that top-level folders represent business capabilities, such as `orders` or `billing`, instead of technical layers such as `controllers` or `services`. Everything one feature needs sits together.

The symptom of the alternative, package by layer, is that a single feature change touches a file in every folder. Adding a field to an order means jumping between `controllers/`, `services/`, `repositories/`, `dtos/` and `validators/`, each holding dozens of unrelated files. The folder tree describes the framework rather than what the application does.

```text
# Package by layer          # Package by feature
src/                        src/
  controllers/                orders/
    orders.ts                   routes.ts
    billing.ts                  place-order.ts
  services/                     order-store.ts
    orders.ts                   index.ts
    billing.ts                billing/
  repositories/                 routes.ts
    orders.ts                   invoice.ts
    billing.ts                  index.ts
```

|                     | By layer                   | By feature                     |
| ------------------- | -------------------------- | ------------------------------ |
| Typical change      | Touches many folders       | Stays in one folder            |
| [Cohesion](#cohesion) | Low, grouped by file type | High, grouped by purpose  |
| Removing a feature  | Search across the tree     | Delete a folder                |
| Team ownership      | Shared across layers       | One team can own a folder      |
| Technical patterns  | Easy to see in one place   | Need shared conventions        |

Folders alone do not create a boundary. Without enforcement, `billing` can import a private file in `orders`, and the features become [coupled](#coupling). Give each feature a public entry point such as `index.ts`, and enforce it with import rules or a tool such as `dependency-cruiser`. Calls between features then go through that interface or through events.

Not everything belongs to a feature. Logging, database connections and design system components go in a small shared area, which should stay free of business logic so it does not become a dumping ground. Layers can still exist inside a feature that is large enough to need them, and small projects can stay flat.

This structure is the folder-level form of [vertical slice architecture](#vertical-slice-architecture). It also makes a later move to a modular monolith or a separate service easier, because the boundaries already exist. Feature folders can also match team boundaries, the alignment described by [Conway's law](#conways-law).

_Usage:_

"Adding a coupon field meant editing seven folders."

"We're organised by layer. Let's move coupon code into a `coupons` feature folder, behind one `index.ts`."

## Section 3 — Creational Patterns

### Factory method

The factory method pattern defines a method for creating an object and lets subclasses decide which concrete class to instantiate. It is one of the creational patterns in the Gang of Four book (1994). Code that needs the object calls the method and depends only on the returned interface.

```typescript
interface Notifier {
  send(to: string, body: string): Promise<void>;
}

abstract class AlertService {
  protected abstract createNotifier(): Notifier;

  async alert(to: string, body: string) {
    await this.createNotifier().send(to, body);
  }
}

class SmsAlertService extends AlertService {
  protected createNotifier() {
    return new SmsNotifier();
  }
}
```

The pattern addresses construction logic spread across call sites. When `new StripeClient(...)` appears in twenty files, or the same `switch (provider)` is copied wherever a client is needed, adding a provider means finding every copy, and a missed copy fails in production. Moving creation behind one method gives that decision a single home and supports the [open-closed principle](#open-closed-principle): a new variant adds a class, and the calling code stays unchanged.

In everyday TypeScript, the term is often used loosely for a plain function such as `createNotifier(config)`. That is a factory function, sometimes called a simple factory. It has no subclass hook, and it is usually the better choice, because inheritance adds [coupling](#coupling) between parent and child. Reserve the class-based form for frameworks where a base class owns the workflow and subclasses supply one part. In that arrangement the factory method is often one step of a [template method](#template-method).

Factory method is often confused with [abstract factory](#abstract-factory). A factory method creates one product. An abstract factory is an object with several creation methods that produce a family of related products.

Skip the pattern when there is only one implementation and no realistic second one. A factory around a single constructor is [speculative generality](#speculative-generality): it adds a level of indirection that every reader must follow.

_Usage:_

"Adding PayPal means editing the provider switch in nine places."

"Move it into one `createPaymentClient` factory and have the nine call sites use that."

### Abstract factory

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

The pattern differs from [factory method](#factory-method) in scope. A factory method creates one product, usually through a subclass hook. An abstract factory is a separate object with several creation methods, usually passed to clients through dependency injection. Implementations of an abstract factory often use factory methods internally.

Avoid it when there is only one family. A `CloudFactory` with a single `AwsFactory` implementation is [premature abstraction](#premature-abstraction), and every new product must then be threaded through an interface that offers no choice.

_Usage:_

"Staging wrote to the local disk but queued jobs on real SQS."

"Those were picked by separate flags. Use one environment factory so they can't diverge."

### Builder pattern

The builder pattern separates the construction of a complex object from the object itself. A builder collects values through a series of method calls, and a final `build()` call validates them and returns the finished object. The Gang of Four book (1994) describes the pattern with a director that runs the steps. Much modern code drops the director and chains calls on the builder.

```typescript
class HttpRequestBuilder {
  private headers: Record<string, string> = {};
  private timeoutMs = 5000;
  private body?: string;

  constructor(private url: string) {}

  header(name: string, value: string) {
    this.headers[name] = value;
    return this;
  }

  timeout(ms: number) {
    this.timeoutMs = ms;
    return this;
  }

  json(data: unknown) {
    this.body = JSON.stringify(data);
    return this.header("Content-Type", "application/json");
  }

  build(): HttpRequest {
    if (this.timeoutMs <= 0) throw new Error("timeout must be positive");
    return new HttpRequest(this.url, { ...this.headers }, this.timeoutMs, this.body);
  }
}
```

The pattern addresses constructors with long parameter lists. A call such as `new Report(id, true, false, null, 30, "pdf")` is hard to read, and swapping two booleans compiles and produces the wrong report. Named builder steps make each value visible, and `build()` gives cross-field rules one place to run, so a half-configured object does not reach the rest of the program.

In TypeScript, an options object usually solves the same problem with less code:

```typescript
new Report({ id, includeCharts: true, format: "pdf" });
```

Use a builder when construction has real steps: values depend on earlier ones, rules span several fields, or the object is assembled across different functions. Query builders and test data builders are common examples. A test builder supplies valid defaults, so each test states only the field it cares about.

A mutable builder has one recurring hazard. Reusing the same instance for two objects can carry headers or filters from the first into the second, so either create a new builder each time or have each step return a copy.

The builder differs from a [factory method](#factory-method). A factory produces an object in one call and chooses which type to create. A builder assembles one object over several calls and focuses on how it is configured.

_Usage:_

"Why did forty tests break when we added a required field to `Order`?"

"Every test constructs it by hand. Add an order builder with valid defaults and only override what each test needs."

### Prototype pattern

The prototype pattern creates new objects by copying an existing instance, called the prototype, instead of constructing each one from scratch. It is a creational pattern from the Gang of Four book (1994). Each prototype exposes a `clone()` method, so code can duplicate an object without knowing its concrete class.

```typescript
interface Cloneable<T> {
  clone(): T;
}

class ChartConfig implements Cloneable<ChartConfig> {
  constructor(
    public title: string,
    public series: string[],
    public colors: Map<string, string>,
  ) {}

  clone() {
    return new ChartConfig(this.title, [...this.series], new Map(this.colors));
  }
}

const base = new ChartConfig("Revenue", ["2025"], new Map([["2025", "blue"]]));
const copy = base.clone();
copy.series.push("2026"); // base is unaffected
```

The pattern is useful when setup is expensive or involves many steps, such as an object configured from a parsed file, or when users duplicate existing items in an editor. A preconfigured instance becomes the starting point, and each copy changes only what differs.

The main failure is the shallow copy. A spread such as `{ ...config }` copies only the top level, so nested arrays and objects remain shared. A user edits the duplicated chart and the original changes too. Each `clone()` must decide which fields are copied and which are deliberately shared.

Generic deep-copy tools have limits. `structuredClone` handles nested data and cycles, but it throws on functions and returns class instances as plain objects without their methods. Objects that hold sockets, file handles or database connections should not be copied at all, and identifiers often need to be regenerated so the copy is not mistaken for the original.

The name overlaps with JavaScript's prototype chain, but they are different mechanisms. The language feature shares behaviour by delegating property lookups to another object. The pattern makes an independent copy of state.

Avoid the pattern when a constructor or [builder](#builder-pattern) can produce the object cheaply. Copying adds a second way to create objects, and every new field must be remembered in `clone()`. A forgotten field appears as a duplicate that silently loses a setting.

_Usage:_

"Duplicating a dashboard and editing it changes the original as well."

"The clone is shallow, so both share the same widgets array. Copy the nested state in `clone()`."

### Singleton

A singleton is a class that allows only one instance and provides a global point of access to it. It is one of the creational patterns in the Gang of Four book (1994). Its use is disputed, because it solves two problems at once: limiting instances and making an object globally reachable.

```typescript
class Config {
  private static instance?: Config;
  private constructor(readonly databaseUrl: string) {}

  static get(): Config {
    return (Config.instance ??= new Config(process.env.DATABASE_URL!));
  }
}
```

The legitimate motive is a resource that should exist once per process, such as a [connection pool](#object-pool), a logger or a metrics client. Creating a new database pool per request quickly produces "too many connections" errors. In JavaScript, a module-level `export const db = createPool()` usually achieves this, because a module is evaluated once per resolved path.

That guarantee has limits. Two versions of a package in `node_modules` produce two instances. Development hot reload can re-evaluate the module and open a new pool on every save. Serverless platforms and multi-process deployments have one instance per process, so a singleton is never a cluster-wide guarantee.

The main cost is hidden [coupling](#coupling). A function that calls `Config.get()` does not declare that dependency in its signature. Tests then leak state into one another: a test passes alone and fails when run after another test that changed the shared instance. Mutable singletons behave like global variables, with the same debugging difficulties.

| Approach                        | Instances           | Dependency visible | Easy to replace in tests |
| ------------------------------- | ------------------- | ------------------ | ------------------------ |
| Classic singleton               | One, enforced       | No                 | No                       |
| Module-level instance           | One per module load | No                 | With module mocking      |
| Created at startup and injected | One, by convention  | Yes                | Yes                      |

The usual alternative is to create the object once at application startup and pass it in through dependency injection. This keeps the single instance and removes the global access. A [service locator](#service-locator) is different again: it centralises lookup, but dependencies stay hidden in the same way.

Stateless, immutable singletons carry little risk and are a reasonable choice.

_Usage:_

"This test only fails when the full suite runs."

"An earlier test changed the `Config` singleton. Inject the config so each test gets its own."

### Object pool

An object pool keeps a set of initialised objects ready for reuse. Code borrows an object, uses it and returns it, so the program avoids repeating expensive creation and destruction. The pattern is not one of the 23 in the Gang of Four book. Database connection pools and thread pools are its common forms.

```typescript
class Pool<T> {
  private waiting: ((item: T) => void)[] = [];

  constructor(private idle: T[]) {}

  acquire(): Promise<T> {
    const item = this.idle.pop();
    if (item !== undefined) return Promise.resolve(item);
    return new Promise((resolve) => this.waiting.push(resolve));
  }

  release(item: T) {
    const next = this.waiting.shift();
    if (next) next(item);
    else this.idle.push(item);
  }
}
```

A pool suits objects that are costly to create, such as a database connection that needs a network handshake and authentication. It also caps usage: a pool of 20 connections stops a traffic spike from opening thousands against the database.

One common failure is pool exhaustion. If a code path throws before releasing a connection, that connection is lost to the pool. After enough errors, requests hang waiting for a connection while the database looks idle. Release in a `finally` block or use a helper that manages the lifetime, and set an acquire timeout so callers fail with a clear error.

```typescript
const conn = await pool.acquire();
try {
  return await conn.query(sql);
} finally {
  pool.release(conn);
}
```

The second failure is leftover state. A reused connection can still carry a session variable or an open transaction from its previous borrower, which then affects an unrelated request. Reset each object on return, and discard any that are broken rather than returning them.

Holding a connection while making a slow external call is a related mistake, because it ties up a scarce resource during work that does not need it.

Do not pool cheap objects. In garbage-collected runtimes, allocating small objects is inexpensive, and a hand-written pool adds state bugs for little gain, so measure first. A pool differs from a [flyweight](#flyweight-pattern): a pooled object is used exclusively by one borrower at a time, while a flyweight is shared by many users at once and must be immutable.

_Usage:_

"The API is hanging, but the database is nearly idle."

"Check the pool. The error path in checkout never releases its connection, so we've run out."

## Section 4 — Structural Patterns

### Adapter pattern

The adapter pattern wraps an object and translates its interface into the one a caller expects. It is a structural pattern from the Gang of Four book (1994). The adapter holds the incompatible object and maps each call, argument and result between the two shapes.

```typescript
interface PaymentGateway {
  charge(amountCents: number, customerId: string): Promise<{ id: string }>;
}

class StripeAdapter implements PaymentGateway {
  constructor(private stripe: Stripe) {}

  async charge(amountCents: number, customerId: string) {
    const intent = await this.stripe.paymentIntents.create({
      amount: amountCents,
      currency: "usd",
      customer: customerId,
    });
    return { id: intent.id };
  }
}
```

The pattern is used when one side of a call cannot change, usually because it is a third-party SDK. Without an adapter, vendor types spread through business logic. When the vendor ships a breaking version or the company switches provider, the change touches dozens of files instead of one class. An adapter confines that vendor knowledge and gives tests a [seam](#seam) where a fake can replace the real client.

Translation must include failure modes as well as method names. If vendor-specific errors escape the adapter, callers end up catching `StripeCardError`, which is a [leaky abstraction](#leaky-abstraction). Map errors to types your application defines. Units, date formats and null handling are other sources of quiet bugs, such as a provider that expects dollars when you send cents.

The structural patterns that wrap an object are often confused:

| Pattern                               | Interface offered                 | Purpose                    |
| ------------------------------------- | --------------------------------- | -------------------------- |
| Adapter                               | Different from the wrapped object | Make incompatible code fit |
| [Decorator](#decorator-pattern) | Same                              | Add behaviour              |
| [Proxy](#proxy-pattern)         | Same                              | Control access             |
| [Facade](#facade-pattern)       | New, simpler                      | Hide a subsystem           |

Between systems, an [anti-corruption layer](#anti-corruption-layer) uses adapters to keep another system's model from entering your own.

Skip the adapter when the dependency is stable, used in one place and already matches your needs. A pass-through class adds a file without isolating anything.

_Usage:_

"Upgrading the Stripe SDK broke forty files."

"Its types are used everywhere. Put it behind a `PaymentGateway` adapter so the next upgrade touches one class."

### Bridge pattern

The bridge pattern splits a concept into two separate hierarchies, an abstraction and an implementation, and connects them through composition. It comes from the Gang of Four book (1994). Each side can then gain new variants without changing the other.

```typescript
interface MessageSender {
  send(to: string, text: string): Promise<void>;
}

class EmailSender implements MessageSender { /* ... */ }
class SlackSender implements MessageSender { /* ... */ }

abstract class Notification {
  constructor(protected sender: MessageSender) {}
  abstract notify(to: string): Promise<void>;
}

class PasswordReset extends Notification {
  notify(to: string) {
    return this.sender.send(to, "Reset your password");
  }
}

class InvoiceDue extends Notification {
  notify(to: string) {
    return this.sender.send(to, "Your invoice is due");
  }
}

new InvoiceDue(new SlackSender());
```

The pattern addresses class explosion, which appears when inheritance is used for two independent dimensions. Classes such as `EmailPasswordReset`, `SlackPasswordReset`, `EmailInvoiceDue` and `SlackInvoiceDue` multiply: three notification types across four channels need twelve classes, and adding one channel means writing three more. With a bridge, the same system has three plus four classes, and a new channel is one class. This applies [composition over inheritance](#composition-over-inheritance).

"Implementation" in this pattern does not mean a concrete subclass of the abstraction. It means the lower-level operations that the abstraction delegates to. A drawing API over interchangeable platform back ends is a typical example.

The bridge is often confused with the [adapter](#adapter-pattern) and [strategy](#strategy-pattern) patterns.

| Pattern  | When applied         | Intent                                |
| -------- | -------------------- | ------------------------------------- |
| Bridge   | Designed up front    | Let two dimensions vary independently |
| Adapter  | Added after the fact | Make an existing interface fit        |
| Strategy | Designed up front    | Swap one algorithm inside an object   |

Code for bridge and strategy can look almost identical. The difference is scope: a strategy replaces one behaviour, while a bridge's implementation supports the abstraction's full set of operations.

Do not introduce a bridge for a dimension that has one variant. A single sender behind an interface is [speculative generality](#speculative-generality). Add the split when a second independent dimension exists.

_Usage:_

"Adding WhatsApp means writing a new class for all eight notification types."

"Channel and message type are separate dimensions. Bridge them so WhatsApp is one sender class."

### Composite pattern

The composite pattern arranges objects in a tree and gives leaves and groups the same interface. It is a structural pattern from the Gang of Four book (1994). A caller can invoke an operation on one item or on an entire subtree without checking which it holds, because each group forwards the call to its children and combines the results.

```typescript
interface FileNode {
  size(): number;
}

class File implements FileNode {
  constructor(private bytes: number) {}
  size() {
    return this.bytes;
  }
}

class Folder implements FileNode {
  private children: FileNode[] = [];
  add(child: FileNode) {
    this.children.push(child);
  }
  size() {
    return this.children.reduce((sum, c) => sum + c.size(), 0);
  }
}
```

The pattern fits data that is naturally hierarchical: file systems, UI component trees, organisation charts, menus, nested permission groups and bundled products in a catalogue. Without it, calling code fills with `if (item.type === "folder")` branches and manual recursion, and each new operation repeats the traversal. A common symptom is logic that handles one or two levels of nesting correctly and breaks when someone creates a third.

The structure has trade-offs. Placing child operations such as `add` on the shared interface makes leaves and groups uniform but forces `File` to implement a method that makes no sense for it, which can violate the [Liskov substitution principle](#liskov-substitution-principle). Placing them only on the group, as above, is safer, at the cost of callers needing to know when they hold a group.

Trees also bring operational risks. A cycle, such as a group containing itself through another group, causes infinite recursion and a stack overflow, so reject cycles when adding children. Very deep or very large trees make a simple `size()` call expensive, and results may need caching and invalidation.

A composite differs from a [decorator](#decorator-pattern), although both forward calls through a shared interface. A decorator wraps exactly one object to add behaviour. A composite holds many children and aggregates their results. To run many unrelated operations across a stable tree, combine it with a [visitor](#visitor-pattern).

Do not use the pattern for flat lists. An array and a loop are enough.

_Usage:_

"Permissions work for nested groups until someone adds a group inside a group inside a group."

"The check only recurses twice. Model groups as a composite so any depth works."

### Decorator pattern

The decorator pattern wraps an object in another object that has the same interface and adds behaviour before or after delegating each call. It is a structural pattern from the Gang of Four book (1994). Callers cannot tell whether they hold the original or a wrapped version, and wrappers can be stacked.

```typescript
interface UserStore {
  find(id: string): Promise<User>;
}

class CachedUserStore implements UserStore {
  private cache = new Map<string, User>();
  constructor(private inner: UserStore) {}

  async find(id: string) {
    const hit = this.cache.get(id);
    if (hit) return hit;
    const user = await this.inner.find(id);
    this.cache.set(id, user);
    return user;
  }
}

const store = new LoggedUserStore(new CachedUserStore(new SqlUserStore(db)));
```

The pattern addresses cross-cutting behaviour that would otherwise bloat a class or multiply subclasses. Adding logging, caching and retries by inheritance produces classes such as `CachedLoggedRetryingUserStore`, one for every combination. Decorators let each concern live in a small class that is composed at startup, following the [open-closed principle](#open-closed-principle) and [composition over inheritance](#composition-over-inheritance).

The order of decorators changes behaviour, and this is a usual source of bugs. A retry wrapper outside a cache repeats the cache check on each attempt, while one inside it repeats only the backend call. Logging outside the cache records every request, while logging inside it records only cache misses, which can make traffic graphs look far lower than reality. Build the stack in one place, so the order is explicit and reviewable.

Every wrapper must also delegate the entire interface. A large interface makes this tedious, and a forgotten method bypasses the added behaviour. Deep stacks lengthen stack traces and make debugging harder.

TypeScript's `@decorator` syntax is a related language feature that modifies classes and methods at definition time. It can implement this pattern but is not the same thing: the object pattern composes at runtime, per instance.

A decorator differs from a [proxy](#proxy-pattern) in intent. A decorator adds behaviour and is usually composed by the caller. A proxy controls access to its subject and often manages that subject's lifecycle.

_Usage:_

"Our request metrics dropped by half after the caching release."

"The logging decorator is now inside the cache, so hits aren't counted. Move it to the outside."

### Facade pattern

The facade pattern provides one simplified interface to a subsystem made of several classes or services. It is a structural pattern from the Gang of Four book (1994). The facade knows which parts to call and in what order, and callers use a small set of operations instead of coordinating those parts themselves.

```typescript
class CheckoutFacade {
  constructor(
    private inventory: Inventory,
    private payments: Payments,
    private shipping: Shipping,
    private email: Email,
  ) {}

  async placeOrder(order: Order) {
    await this.inventory.reserve(order.items);
    const payment = await this.payments.charge(order.total, order.customerId);
    const label = await this.shipping.createLabel(order.address);
    await this.email.sendConfirmation(order.customerId, payment.id, label.tracking);
  }
}
```

The pattern addresses workflows that every caller must reassemble. When the web handler, an admin script and a background job each call the same four services in sequence, they drift apart. One forgets to reserve stock, or sends the email before charging, and the resulting bug appears only through that entry point. A facade puts the sequence in one place and reduces [coupling](#coupling) between callers and the subsystem's internals. A well-designed facade resembles a [deep module](#deep-module): a small interface in front of substantial behaviour.

A facade does not usually prevent direct access to the subsystem. Callers with an unusual need can still reach the underlying classes. If isolation is required, enforce it through module boundaries.

The main risk is growth. A facade that collects every operation in a domain becomes a [god object](#god-object) that changes for every feature. Split it by use case when its methods stop relating to one another. A facade that only forwards each call to one method adds a layer with no benefit.

It is often confused with two related patterns:

| Pattern                             | Wraps                | Purpose                                 |
| ----------------------------------- | -------------------- | --------------------------------------- |
| Facade                              | Several objects      | Simplify use of a subsystem             |
| [Adapter](#adapter-pattern)   | Usually one object   | Convert to an expected interface        |
| [Mediator](#mediator-pattern) | Several peer objects | Coordinate peers, which talk through it |

A mediator also differs in direction. Subsystem classes do not know a facade exists, while colleagues actively send messages to their mediator.

A [service layer](#service-layer) often plays the facade role for an application's domain logic.

_Usage:_

"The admin tool created an order without reserving stock."

"It calls the services by hand. Route it through the checkout facade like the API does."

### Flyweight pattern

The flyweight pattern reduces memory use by sharing the common, immutable state of many similar objects. It is a structural pattern from the Gang of Four book (1994). The pattern divides each object's data in two: intrinsic state, which is identical across many objects and can be shared, and extrinsic state, which varies per use and is stored by the caller or passed in.

```typescript
class TreeType {
  constructor(readonly species: string, readonly texture: Uint8Array) {}
  draw(x: number, y: number) { /* render texture at x, y */ }
}

class TreeTypes {
  private types = new Map<string, TreeType>();

  get(species: string, load: () => Uint8Array) {
    let type = this.types.get(species);
    if (!type) {
      type = new TreeType(species, load());
      this.types.set(species, type);
    }
    return type;
  }
}

const trees = [{ x: 10, y: 20, type: types.get("oak", loadOak) }];
```

The pattern addresses programs that run out of memory because they hold large numbers of near-identical objects. A map with a million markers, each carrying its own copy of an icon, or a text editor storing font data per character, can crash a browser tab or trigger long garbage collection pauses. Sharing one `TreeType` across a million trees leaves each tree holding only coordinates and a reference.

Shared state must be immutable. If one caller mutates a flyweight, every object using it changes at once, and the bug appears in an unrelated part of the screen. Mark fields `readonly` and freeze objects where appropriate.

The pattern has costs. The factory's cache can grow indefinitely if keys are unbounded, creating a leak while trying to save memory. Code becomes harder to follow because an object's data now lives in two places, and computing extrinsic state on each call can cost CPU time.

Measure with a heap profile before applying it. If there are thousands of objects rather than millions, or little data is actually duplicated, the pattern adds complexity for a negligible saving.

A flyweight differs from an [object pool](#object-pool). A pooled object is mutable and used by one borrower at a time, while a flyweight is used by many at the same moment. It also differs from a [singleton](#singleton), which has one instance overall, whereas a flyweight factory holds one instance per distinct key.

_Usage:_

"The map tab dies at around 200,000 markers."

"Each marker holds its own copy of the icon bitmap. Share one flyweight per icon type and store only positions."

### Proxy pattern

The proxy pattern places a stand-in object in front of another object, called the subject, and gives it the same interface. It is a structural pattern from the Gang of Four book (1994). The proxy receives each call and decides whether, when and how to forward it.

```typescript
interface ReportService {
  generate(id: string): Promise<Report>;
}

class AuthorizedReportService implements ReportService {
  constructor(private real: ReportService, private user: User) {}

  async generate(id: string) {
    if (!this.user.can("reports:read")) throw new ForbiddenError();
    return this.real.generate(id);
  }
}
```

Proxies are commonly grouped by what they control:

| Type            | Controls    | Example                                           |
| --------------- | ----------- | ------------------------------------------------- |
| Virtual         | Creation    | Load a large object on first use                  |
| Protection      | Permission  | Check the caller's rights                         |
| Remote          | Location    | Client stub that calls a service over the network |
| Caching         | Repeat work | Return a stored response                          |
| Smart reference | Bookkeeping | Count references or log access                    |

The main hazard is that a proxy makes expensive or unreliable work look like an ordinary method call. An ORM using [lazy load](#lazy-load) returns proxy objects, so reading `order.customer.name` in a loop looks harmless but issues one database query per row, and a page gets slower as data grows. A remote proxy has the same problem: a call that reads as local can time out or fail partway. This is a form of [leaky abstraction](#leaky-abstraction), so make remote and lazy calls visible in names or types where it matters.

JavaScript has a built-in `Proxy` object that intercepts property access and method calls. Libraries use it for reactive state and mocks. It is one way to implement the pattern, but it adds overhead and has identity surprises: a proxy and its target are different objects under `===`, and class private `#fields` throw a `TypeError` when accessed through a proxy.

A proxy differs from a [decorator](#decorator-pattern) in intent, even though the code can look identical. A decorator adds behaviour and is stacked by the caller. A proxy controls access to its subject and may create or manage that subject itself. An [adapter](#adapter-pattern) differs by changing the interface, while a proxy keeps it.

Skip a proxy when a plain function call at the boundary does the job, such as a permission check in one handler.

_Usage:_

"This endpoint runs 400 queries to render a list of 400 orders."

"`order.customer` is a lazy proxy. Eager-load customers in the original query."

## Section 5 — Behavioral Patterns

### Chain of responsibility

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

Chain of responsibility differs from the [decorator](#decorator-pattern), which has a similar structure. A decorator adds behaviour around one wrapped object and normally still produces its result. A chain handler may reject the request and end processing. It also differs from [pipes and filters](#pipes-and-filters), in which each stage transforms data and passes it on, with no handler claiming the request.

For two or three fixed checks, ordinary `if` statements are clearer.

_Usage:_

"Requests to the upload route hang with no error."

"The new quota middleware never calls `next` when the user is under the limit."

### Command pattern

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

Inverse operations can be difficult to write. Deleting a record may cascade, and sending an email cannot be reversed. For those steps, capture a snapshot with a [memento](#memento-pattern) or mark the command as not undoable.

A command differs from a [strategy](#strategy-pattern). A strategy supplies a way of doing a job the context already owns. A command represents a specific action, with its arguments, to be done at some point. The word "command" in [command-query separation](#command-query-separation) and CQRS is related, but it refers to an operation that changes state rather than this object structure.

Avoid the pattern when an action is only ever invoked directly. A plain function is enough.

_Usage:_

"Undo only works for about half of the editor's actions."

"The rest mutate state in their click handlers. Move them to commands with an `undo` method."

### Interpreter pattern

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

The pattern suits a small, stable language that must be evaluated repeatedly, such as pricing rules, search filters, feature-flag conditions or permission policies. A typical trigger is a config format that grows by accident: a JSON filter gains `and`, then `or`, then nested groups, and the evaluation code becomes a tangle of special cases. Naming the grammar turns that into a defined set of node types. The resulting tree is an instance of the [composite](#composite-pattern) pattern.

The pattern describes evaluation and does not cover parsing. Text such as `age > 18 AND score > 700` still needs a parser to produce the tree, and that parser is often the larger piece of work.

Costs rise with the size of the grammar. One class per rule becomes hard to maintain for a large language, and walking a tree is slower than running compiled code. For anything substantial, use a parser generator or an existing language such as SQL or an embedded scripting engine. For combining business rules in code, the [specification pattern](#specification-pattern) is a narrower option built on the same idea.

Do not implement this by passing user input to `eval`, which gives that input access to the entire runtime. A dedicated interpreter can only do what its node types allow. Limit expression depth and size as well, so a crafted rule cannot exhaust CPU or the stack.

When many operations are needed on the tree, a [visitor](#visitor-pattern) keeps them out of the node classes.

_Usage:_

"Our discount rules JSON has grown nested `or` blocks and nobody can tell how they evaluate."

"It's a language now. Define the node types and write a small interpreter instead of more special cases."

### Iterator pattern

The iterator pattern provides a way to access the elements of a collection in sequence without exposing how the collection is stored. It is a behavioural pattern from the Gang of Four book (1994). An iterator tracks the current position and hands out one element at a time, so the same loop can work over an array, a tree, a file or a paginated API.

JavaScript builds the pattern into the language. An object is iterable if it has a `Symbol.iterator` method, and generator functions produce iterators with little code. `for...of`, array spread and array destructuring all use this protocol.

```typescript
async function* allOrders(api: OrdersApi) {
  let cursor: string | undefined;
  do {
    const page = await api.list({ cursor, limit: 100 });
    yield* page.items;
    cursor = page.nextCursor;
  } while (cursor);
}

for await (const order of allOrders(api)) {
  if (order.total > 10_000) {
    flag(order);
    break;
  }
}
```

A common reason to use an iterator is a job that loads an entire table or API result into an array and runs out of memory once the data grows. An iterator fetches one page at a time, holds little in memory and can stop early: the `break` above means later pages are never requested.

Iterators have a few recurring surprises:

| Behaviour                       | Symptom                                                            |
| ------------------------------- | ------------------------------------------------------------------ |
| Generators are single-use       | A second loop over the same object yields nothing                  |
| Evaluation is lazy              | Errors appear during iteration, not where the iterator was created |
| Source changes during traversal | Elements are skipped or repeated                                   |
| Early exit needs cleanup        | A file or cursor stays open unless `finally` releases it           |

The last row has a language-level answer: `for...of` calls the iterator's `return` method on `break`, which runs any `finally` block in a generator.

An iterator differs from a [visitor](#visitor-pattern). An iterator controls the order of traversal and leaves the work to the caller. A visitor defines per-type operations that run over a structure, and the traversal can be kept elsewhere.

Exposing an iterator also helps [encapsulation](#encapsulation): a class can offer iteration over its items without returning the private array, which callers could mutate.

Skip custom iterators for small in-memory arrays, where `map` and `filter` are clearer.

_Usage:_

"The export job gets OOM-killed now that we have two million rows."

"It loads them all first. Iterate with a cursor and write one batch at a time."

### Mediator pattern

The mediator pattern places a coordinator between a group of objects, called colleagues, so that they communicate through it instead of referring to each other directly. It is a behavioural pattern from the Gang of Four book (1994). Each colleague knows only the mediator, and the mediator holds the rules for how they interact.

```typescript
interface CheckoutMediator {
  notify(event: "countryChanged" | "couponApplied"): void;
}

class CheckoutForm implements CheckoutMediator {
  constructor(
    private shipping: ShippingPicker,
    private tax: TaxSummary,
    private total: OrderTotal,
  ) {}

  notify(event: "countryChanged" | "couponApplied") {
    if (event === "countryChanged") this.shipping.reload();
    this.tax.recalculate();
    this.total.refresh();
  }
}
```

The pattern addresses a web of direct references. In a form where the country field updates shipping, shipping updates tax, tax updates the total and the coupon field touches all three, each component imports its neighbours. Changing one breaks others, none can be reused alone, and a [circular dependency](#circular-dependency) can appear. Connecting n objects to one another requires up to n(n-1)/2 links. With a mediator, it takes n.

Interaction logic then lives in a single class, which is easier to read and change, and each colleague has lower [coupling](#coupling). A parent component that holds shared state and passes callbacks to its children is a familiar example in UI frameworks.

The risk is that the mediator absorbs everything. As rules accumulate, it can turn into a [god object](#god-object) that every feature must edit. Keep it limited to coordination, leave business rules in the colleagues or domain objects, and split it when it serves unrelated workflows.

The mediator is often compared with two other patterns:

| Pattern                             | Who knows whom                                  | Direction              |
| ----------------------------------- | ----------------------------------------------- | ---------------------- |
| Mediator                            | Colleagues know the mediator, which knows them  | Two-way coordination   |
| [Observer](#observer-pattern) | Subject does not know what its observers do     | One-way notification   |
| [Facade](#facade-pattern)     | Callers know the facade; the subsystem does not | One-way simplification |

A mediator is often implemented with observers: colleagues emit events and the mediator listens. The distinction is that a mediator holds the coordination logic, while plain observers react independently.

Do not add a mediator for two objects that interact in one simple way. A direct call is easier to follow.

_Usage:_

"Changing the country picker broke the coupon field again."

"They all call each other. Have the form mediate, so each field only reports that it changed."

### Memento pattern

The memento pattern captures an object's internal state in a snapshot that can restore the object later, without exposing that state to other code. It is a behavioural pattern from the Gang of Four book (1994). It has three roles: the originator creates and restores snapshots, the memento holds the state, and the caretaker stores mementos without reading them.

```typescript
class Memento {
  constructor(readonly state: Readonly<{ text: string; cursor: number }>) {}
}

class Editor {
  private text = "";
  private cursor = 0;

  save() {
    return new Memento({ text: this.text, cursor: this.cursor });
  }
  restore(m: Memento) {
    this.text = m.state.text;
    this.cursor = m.state.cursor;
  }
  type(value: string) {
    this.text += value;
    this.cursor += value.length;
  }
}

const history: Memento[] = [];
history.push(editor.save());
editor.type("hello");
editor.restore(history.pop()!);
```

The pattern suits undo, draft recovery, checkpoints in multi-step wizards and rollback after a failed operation. It preserves [encapsulation](#encapsulation): the class that owns the state decides what a snapshot contains, so a history manager does not need access to private fields.

The usual bug is a snapshot that shares references with live state. If a memento stores `this.items` instead of a copy, later edits change the snapshot too, and undo appears to do nothing or restores a half-changed document. Copy mutable state when saving, or keep state immutable so a snapshot can be a reference.

Memory is the second constraint. Saving a large document after each keystroke grows quickly, and long sessions can slow or crash a tab. Cap the history, group rapid changes into one entry, or use structural sharing so that snapshots reuse unchanged data.

Persisted mementos add a versioning problem. A draft saved by last month's release may not match today's shape, so include a schema version and a migration path, or discard old snapshots deliberately. External effects are not restored either: rolling an object back does not unsend an email.

Memento is the alternative to inverse operations in the [command](#command-pattern) pattern:

| Approach          | Stores                     | Suits                                      |
| ----------------- | -------------------------- | ------------------------------------------ |
| Memento           | Full state                 | Changes that are hard to reverse           |
| Command with undo | The change and its inverse | Large state with small, reversible changes |

The two are often combined, with each command holding a memento of what it altered. For simple state, a plain immutable value in a history array is enough and needs no dedicated classes.

_Usage:_

"Undo restores the title but leaves the edited table cells."

"The snapshot holds a reference to the cells array. Deep-copy it when saving the memento."

### Observer pattern

The observer pattern lets objects subscribe to a subject and receive a notification when the subject changes. It is a behavioural pattern from the Gang of Four book (1994). The subject keeps a list of observers and calls each one, without knowing what they do.

```typescript
type Listener<T> = (value: T) => void;

class Subject<T> {
  private listeners = new Set<Listener<T>>();

  subscribe(listener: Listener<T>) {
    this.listeners.add(listener);
    return () => this.listeners.delete(listener);
  }

  emit(value: T) {
    for (const listener of this.listeners) listener(value);
  }
}
```

The pattern lets a change in one module trigger behaviour in others without the first module importing them. An order module can emit `orderPlaced`, and email, analytics and inventory can each subscribe, which reduces [coupling](#coupling) and lets new reactions be added without editing the subject. DOM events, Node's `EventEmitter` and reactive UI libraries all use it.

The pattern has several recurring failures:

| Failure               | Symptom                                                            | What to do                                 |
| --------------------- | ------------------------------------------------------------------ | ------------------------------------------ |
| Forgotten unsubscribe | Memory grows, Node prints `MaxListenersExceededWarning`            | Return and call a cleanup function         |
| Listener throws       | Later listeners never run, and the emitter's caller sees the error | Catch per listener where isolation matters |
| Cascading updates     | One change triggers a chain of notifications or an infinite loop   | Avoid emitting from inside a listener      |

Observers also hide control flow. Reading `order.place()` does not reveal what runs afterwards, so a slow listener can delay the request with no visible cause in the calling code. Log or trace listeners.

In-process observers are not durable. If the process crashes after the database commit but before a listener finishes, that work is lost. For work that must happen, such as sending a receipt, use a persisted approach such as the outbox pattern.

The observer differs from publish-subscribe. An observer subject holds direct references to its subscribers in one process. Publish-subscribe places a broker between them, so neither side knows the other and the two can run on separate machines. A [mediator](#mediator-pattern) differs in that it holds coordination logic, whereas a subject only announces a change. A [domain event](#domain-event) is a common payload for this mechanism.

Use a direct call when one module must always invoke exactly one other.

_Usage:_

"Memory climbs every time someone opens and closes the chat panel."

"The panel subscribes on mount and never unsubscribes. Return a cleanup function from the effect."

### State pattern

The state pattern moves behaviour that depends on an object's state into separate state objects. It is a behavioural pattern from the Gang of Four book (1994). The main object, called the context, delegates to its current state object, so it appears to change behaviour when the state changes.

```typescript
interface OrderState {
  pay(order: Order): void;
  ship(order: Order): void;
}

class Pending implements OrderState {
  pay(order: Order) {
    order.setState(new Paid());
  }
  ship() {
    throw new Error("Cannot ship an unpaid order");
  }
}

class Paid implements OrderState {
  pay() {
    throw new Error("Already paid");
  }
  ship(order: Order) {
    order.setState(new Shipped());
  }
}

class Shipped implements OrderState {
  pay() {
    throw new Error("Already paid");
  }
  ship() {
    throw new Error("Already shipped");
  }
}

class Order {
  private state: OrderState = new Pending();
  setState(state: OrderState) {
    this.state = state;
  }
  pay() {
    this.state.pay(this);
  }
  ship() {
    this.state.ship(this);
  }
}
```

The pattern addresses the same `switch (status)` repeated in every method. When a new status such as `refunded` is added, each switch must be updated, and a missed branch lets an order ship twice or be refunded before it was paid. With state objects, all behaviour for one status lives in one class, and the legal transitions are explicit. An illegal transition fails at the point it is attempted, which protects the object's [invariants](#invariant).

In TypeScript, classes are often unnecessary. A discriminated union with a `transition(state, event)` function and an exhaustive `switch` produces compiler errors for missed cases and keeps state as plain data. This is usually the better choice when state is persisted, because class instances must be rebuilt from a database column anyway. For workflows with many states, guards and timers, a state machine library adds a formal model.

The state pattern is structurally almost identical to the [strategy pattern](#strategy-pattern). The difference is in who changes the object in use:

|                         | State                         | Strategy                   |
| ----------------------- | ----------------------------- | -------------------------- |
| Selected by             | The object's own transitions  | The caller, usually once   |
| Objects know each other | Often, to trigger transitions | No                         |
| Models                  | A lifecycle                   | Interchangeable algorithms |

Two or three statuses with a small amount of conditional logic do not need this pattern, because the indirection outweighs the benefit. Introduce it when the same status checks appear across many methods or when invalid transitions have caused bugs.

_Usage:_

"A cancelled order got shipped because `ship()` didn't check for the new status."

"Status checks are scattered across every method. Model the lifecycle as explicit states so illegal transitions fail."

### Strategy pattern

The strategy pattern defines a family of interchangeable algorithms behind one interface, so the code that uses them can switch between them without changing. It is a behavioural pattern from the Gang of Four book (1994). The object that uses an algorithm, called the context, holds a reference to a strategy and delegates that part of its work.

```typescript
type PricingStrategy = (subtotal: number) => number;

const standard: PricingStrategy = (subtotal) => subtotal;
const member: PricingStrategy = (subtotal) => subtotal * 0.9;
const bulk: PricingStrategy = (subtotal) => (subtotal > 1000 ? subtotal * 0.8 : subtotal);

function checkout(cart: Cart, pricing: PricingStrategy) {
  return pricing(cart.subtotal) + cart.shipping;
}
```

In languages with first-class functions, a strategy is often a plain function, as above, and needs no class hierarchy. Use a class or object when the strategy needs configuration, holds state or has several related methods.

The pattern addresses branching that keeps growing. A `calculatePrice` function with an `if` for each customer tier gets longer with every promotion, each edit risks breaking existing tiers, and the tests must cover all paths through one function. Separate strategies can be added without changing the context, in line with the [open-closed principle](#open-closed-principle), and each can be tested alone.

Selection still has to happen somewhere. Put the mapping from configuration to strategy in one place, such as a lookup table or [factory method](#factory-method), so the conditional is not copied to every call site. All strategies must also honour the same contract. If one returns cents while another returns dollars, the type checker accepts both and the caller gets wrong totals, a violation of the [Liskov substitution principle](#liskov-substitution-principle).

The strategy is commonly confused with two patterns:

| Pattern                                   | What varies                    | How                               |
| ----------------------------------------- | ------------------------------ | --------------------------------- |
| Strategy                                  | A complete algorithm           | Composition, chosen by the caller |
| [State](#state-pattern)             | Behaviour across a lifecycle   | The object transitions itself     |
| [Template method](#template-method) | Steps within a fixed algorithm | Inheritance                       |

Do not introduce strategies when there are two branches that rarely change. A single `if` is easier to read than an interface, several implementations and a selection mechanism, and extracting it early is [premature abstraction](#premature-abstraction).

_Usage:_

"Every new promotion means another branch in `calculatePrice`, and last week's broke member pricing."

"Make each pricing rule a strategy and select it from a lookup table."

### Template method

The template method pattern defines the outline of an algorithm in a base class method and lets subclasses supply some of its steps. It is a behavioural pattern from the Gang of Four book (1994). The base class controls the order of the steps, and subclasses override only the ones that vary. Optional steps with a default empty body are called hooks.

```typescript
abstract class DataImport {
  async run(path: string) {
    const raw = await this.read(path);
    const rows = this.parse(raw);
    this.validate(rows);
    await this.save(rows);
    await this.afterSave(rows);
  }

  protected abstract parse(raw: string): Row[];
  protected async afterSave(_rows: Row[]) {} // hook

  private read(path: string) {
    return readFile(path, "utf8");
  }
  private validate(rows: Row[]) { /* shared rules */ }
  private async save(rows: Row[]) { /* shared persistence */ }
}

class CsvImport extends DataImport {
  protected parse(raw: string) {
    return parseCsv(raw);
  }
}
```

The pattern removes duplication among workflows that differ in a few steps. If CSV, JSON and XML imports each copy the same read, validate and save sequence, a fix to validation may reach two of the three, and one format keeps accepting bad rows. With a template method, the sequence exists once. Test frameworks use the same structure for lifecycle methods such as `setUp` and `tearDown`, which the framework calls and a subclass provides. This is a form of [inversion of control](#inversion-of-control).

The main cost comes from inheritance. Subclasses depend on the base class's internals and call order, so a small base-class change can break a subclass in a distant file. Reading the flow requires jumping between parent and child. Overrides that must remember to call `super.method()` are a frequent source of bugs, and a class can inherit from only one parent, so two independent variations cannot be combined.

Limit the number of abstract steps, and treat the template itself as non-overridable by convention. TypeScript has no `final` keyword, so a subclass can still replace `run`.

The pattern differs from the [strategy pattern](#strategy-pattern) in mechanism. A template method varies steps through inheritance, fixed when the class is defined. A strategy varies behaviour through composition and can be swapped at runtime. When variation grows, following [composition over inheritance](#composition-over-inheritance) usually means passing the steps as functions:

```typescript
async function runImport(path: string, parse: (raw: string) => Row[]) { /* ... */ }
```

That version is often simpler in TypeScript, so prefer it unless a framework requires subclassing.

_Usage:_

"We fixed the date validation, but XML imports still accept bad dates."

"XML has its own copy of the flow. Move the shared steps into one template and override only parsing."

### Visitor pattern

The visitor pattern moves an operation out of a group of classes and into a separate visitor object that has one method per class. It is a behavioural pattern from the Gang of Four book (1994). Each element implements `accept(visitor)` and calls the visitor method for its own type. This technique, called double dispatch, selects the code to run from both the element's type and the visitor's type.

```typescript
interface ShapeVisitor<R> {
  visitCircle(shape: Circle): R;
  visitSquare(shape: Square): R;
}

class Circle {
  constructor(readonly radius: number) {}
  accept<R>(visitor: ShapeVisitor<R>) {
    return visitor.visitCircle(this);
  }
}

class Square {
  constructor(readonly side: number) {}
  accept<R>(visitor: ShapeVisitor<R>) {
    return visitor.visitSquare(this);
  }
}

const area: ShapeVisitor<number> = {
  visitCircle: (c) => Math.PI * c.radius ** 2,
  visitSquare: (s) => s.side ** 2,
};
```

The pattern addresses operations that keep landing on stable classes. In a compiler, the syntax node types change rarely, but type checking, linting, formatting and code generation all need to handle each node. Placing all of that on the nodes bloats them. The alternative is `instanceof` chains across the codebase, where a new node type is silently ignored by any chain that was not updated. With a visitor, adding a method to the interface produces a compile error in every visitor that lacks it. ESLint rules and Babel plugins use a visitor-style API keyed by node type.

The design makes one kind of change easy at the expense of another:

| Change              | With visitor       | With methods on each class |
| ------------------- | ------------------ | -------------------------- |
| Add an operation    | One new visitor    | Edit every class           |
| Add an element type | Edit every visitor | One new class              |

Use it only when the element types are stable. Visitors also often need access to element internals, which can weaken [encapsulation](#encapsulation).

In TypeScript, a discriminated union and an exhaustive `switch` usually give the same benefits with less ceremony, since there is no `accept` and the compiler still reports unhandled cases:

```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "square"; side: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side ** 2;
  }
}
```

A visitor differs from an [iterator](#iterator-pattern): an iterator provides the next element, while a visitor defines what to do with each type of element. It is often applied across a [composite](#composite-pattern) tree.

_Usage:_

"We added a new AST node and the formatter silently dropped it."

"The formatter uses `instanceof` checks. Make it a visitor so a new node type is a compile error."

### Null object pattern

The null object pattern replaces a missing collaborator with an object that implements the same interface and does nothing, or returns a neutral value. Callers use it like any other implementation and do not check for absence. It is not one of the 23 patterns in the Gang of Four book.

```typescript
interface Logger {
  info(message: string): void;
}

class ConsoleLogger implements Logger {
  info(message: string) {
    console.log(message);
  }
}

class NullLogger implements Logger {
  info() {}
}

class ImportJob {
  constructor(private logger: Logger = new NullLogger()) {}

  run() {
    this.logger.info("starting");
  }
}
```

The pattern addresses optional dependencies that force a check at each use. Code fills with `if (logger) logger.info(...)`, and the one call that omits the check crashes with `Cannot read properties of undefined`, often in an error path that rarely runs. A null object removes those branches because there is always a valid object to call. Neutral values work the same way: an empty list, a zero discount or a guest user whose permissions are all false.

The main danger is hiding a real failure. A silent logger is harmless. A `NullPaymentGateway` used because a production config key is missing means orders are marked paid with no charge, and nothing raises an error. Use the pattern only when doing nothing is a correct outcome for the business. If absence means something is wrong, fail at startup or throw.

| Situation                                   | Better choice                  |
| ------------------------------------------- | ------------------------------ |
| Optional logging, metrics or tracing        | Null object                    |
| Empty collection                            | Return an empty array          |
| Record not found, and the caller must react | Return `null` or a result type |
| Required dependency is missing              | Fail at startup                |

In TypeScript with `strictNullChecks`, the compiler already forces callers to handle `null`, and optional chaining such as `logger?.info()` is short. That lowers the need for this pattern in small cases.

A null object differs from a test stub, even though both can be empty classes. A stub exists for tests, while a null object is a legitimate production behaviour. It is often a [strategy](#strategy-pattern) that performs no work. It honours the [Liskov substitution principle](#liskov-substitution-principle) only if callers do not depend on the action having taken place.

_Usage:_

"Orders were marked paid all weekend with no charges in Stripe."

"The missing key fell back to `NullPaymentGateway`. Payments must fail at startup instead of doing nothing."

## Section 6 — Enterprise Application Patterns

### Transaction script

A transaction script is a single procedure that handles one request from start to finish. It validates input, applies the business rules, reads and writes the database, and returns a result. Martin Fowler named the pattern in Patterns of Enterprise Application Architecture (2002). An application built this way has roughly one script per use case, often a route handler or a function in a services file.

```typescript
async function cancelOrder(db: Db, orderId: string) {
  await db.transaction(async (tx) => {
    const order = await tx.orders.find(orderId);
    if (!order) throw new NotFound();
    if (order.status === "shipped") throw new Conflict("Already shipped");

    await tx.orders.update(orderId, { status: "cancelled" });
    await tx.refunds.insert({ orderId, amount: order.total });
  });
}
```

The pattern suits simple logic. Each use case reads top to bottom, there is little indirection, and a developer can find a feature by finding its endpoint. For CRUD applications, internal tools and integrations that mostly move data, it is often the appropriate design, and more structure would add cost without protecting any rule.

The cost appears when rules start to interact. The check that a shipped order cannot be cancelled gets copied into the refund script, the admin script and the bulk import. When the rule changes, one copy is missed, and support finds an order refunded after it shipped. Shared helper functions delay this problem, but no single place owns the rule.

At that point, consider moving the affected logic into a [domain model](#domain-model), where the object that holds the data also enforces its rules. The move can be gradual: extract one rule at a time and leave simple scripts alone.

| Question               | Transaction script            | Domain model                      |
| ---------------------- | ----------------------------- | --------------------------------- |
| Where do rules live?   | In each procedure             | On objects that own the data      |
| Best fit               | Simple, independent use cases | Rules shared across use cases     |
| Cost of starting       | Low                           | Higher                            |
| Failure as logic grows | Duplicated conditionals       | Over-modelling when rules are few |

A transaction script is often confused with an [anemic domain model](#anemic-domain-model). Both keep logic in procedures, but the anemic version also maintains domain classes that carry no behaviour, paying for the structure without receiving its benefit.

_Usage:_

"Cancelling from the admin panel still refunds shipped orders."

"The check only exists in the customer-facing script. Move it onto `Order` so both paths use it."

### Domain model

A domain model is a set of objects that represent the concepts of a business, with each object holding both its data and the rules that apply to that data. An `Order` knows whether it can be cancelled, and calling code asks it to cancel instead of editing a status field. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002), and Eric Evans built a modelling practice around it in Domain-Driven Design (2003).

```typescript
class Order {
  private status: "open" | "shipped" | "cancelled" = "open";

  constructor(private readonly lines: OrderLine[]) {}

  cancel(): Refund {
    if (this.status === "shipped") throw new OrderAlreadyShipped();
    this.status = "cancelled";
    return Refund.forLines(this.lines);
  }
}
```

The pattern addresses business rules scattered across handlers. When the cancellation check lives in four [transaction scripts](#transaction-script), a rule change needs four edits, and the missed one appears as a refund on a shipped order. In a domain model, the rule has one location, and [encapsulation](#encapsulation) stops other code from bypassing it. Conditions that must always hold, known as [invariants](#invariant), can be checked by the object that owns the state.

A domain model has costs. Objects shaped around business concepts rarely match database tables, so persistence usually needs a [data mapper](#data-mapper). The team also has to learn the business well enough to model it, and early models are often wrong and need reshaping. For an application that mostly stores and displays records, this structure adds ceremony without protecting any rule, and transaction scripts or [active record](#active-record) are simpler.

The term is also used loosely for any diagram or set of classes describing a business. In the pattern sense, data classes with public setters and all logic held in services do not qualify. That arrangement is an [anemic domain model](#anemic-domain-model), which carries the cost of the extra classes without keeping rules beside the data.

A practical approach is to apply a domain model only to the parts of a system where rules are complicated or change often, and leave the rest simple. Names in the model should match the [ubiquitous language](#ubiquitous-language) that domain experts use.

_Usage:_

"Where does the rule for cancelling an order live?"

"In four handlers. Move it onto `Order` so there is one version to change."

### Service layer

A service layer is the set of application operations that sits between callers, such as controllers, CLI commands and queue consumers, and the business logic underneath. Each operation represents one use case, such as `placeOrder` or `cancelSubscription`, and coordinates loading data, calling domain objects, committing a transaction and triggering side effects. Martin Fowler's Patterns of Enterprise Application Architecture (2002) catalogues the pattern.

```typescript
class OrderService {
  constructor(private uow: UnitOfWork, private mailer: Mailer) {}

  async cancel(orderId: OrderId, actor: UserId) {
    const order = await this.uow.orders.get(orderId);
    const refund = order.cancel(actor);
    await this.uow.refunds.add(refund);
    await this.uow.commit();
    await this.mailer.sendCancellation(order);
  }
}
```

The pattern addresses one operation being implemented several times. When checkout logic lives in an HTTP controller, the nightly job and the admin CLI either call the endpoint over HTTP or copy the code, and the copies drift. With a service layer, all three call the same method, and the controller only parses the request and formats the response. The operation is also a natural place to hold a [unit of work](#unit-of-work).

A service layer should coordinate rather than decide. When it accumulates conditionals about order state, the domain objects become data holders and the design has moved towards an [anemic domain model](#anemic-domain-model). A single `OrderService` of several thousand lines is a common sign, and is a form of [god object](#god-object). Split services by use case and push rules down onto the objects that own the data.

The pattern is often confused with two similar ones:

| Concept                                | Responsibility                       | Example                |
| -------------------------------------- | ------------------------------------ | ---------------------- |
| Service layer                          | Orchestrates a use case              | `OrderService.cancel`  |
| [Domain service](#domain-service) | Holds a rule spanning domain objects | `DiscountPolicy.quote` |
| [Facade](#facade-pattern)        | Simplifies a subsystem's interface   | `Payments.charge`      |

A small application with one delivery mechanism does not need this layer. A route handler written as a [transaction script](#transaction-script) is simpler until a second caller appears, and extracting a service at that point is a small refactor. Adding a service that only forwards each call to a repository creates indirection with no benefit.

_Usage:_

"The CLI refund skips the fraud check that the API runs."

"Each has its own copy. Move refunds into the service layer and have both call it."

### Active record

Active record is a pattern in which an object wraps one database row, holding the row's columns as fields along with the domain logic and the methods that load and save it. A `User` instance has an `email` property, a `confirm()` method and a `save()` method. Martin Fowler named the pattern in Patterns of Enterprise Application Architecture (2002), and Ruby on Rails adopted the name for its ORM.

```typescript
class User extends Model {
  email!: string;
  confirmedAt: Date | null = null;

  confirm() {
    this.confirmedAt = new Date();
    return this.save();
  }
}

const user = await User.findById(id);
await user.confirm();
```

The pattern suits applications whose objects map closely to tables. It needs little code, new developers can follow it quickly, and frameworks such as Rails and Laravel's Eloquent provide queries, validations and migrations around it. For many CRUD products it is a productive default.

The trade-offs appear as the domain diverges from the schema. Because persistence is part of the object, business logic is hard to test without a database or a stubbed framework. Lifecycle callbacks add hidden behaviour: a script that updates one column sends a welcome email because an `afterSave` hook fired. Models also tend to grow into [god objects](#god-object), since every feature that touches users adds methods to `User`.

| Concern               | Active record             | [Data mapper](#data-mapper)       |
| --------------------- | ------------------------- | --------------------------------------- |
| Who saves the object  | The object itself         | A separate mapper                       |
| Object shape          | Mirrors the table         | Can differ from the table               |
| Testing domain logic  | Usually needs a database  | Plain objects                           |
| Setup cost            | Low                       | Higher                                  |
| Fits                  | Schema-shaped domains     | A complex [domain model](#domain-model) |

To contain the costs, reserve callbacks for data integrity, move workflows that span models into a [service layer](#service-layer), and extract complicated rules into plain objects. Migrating from active record to a data mapper later is expensive, because calling code across the application depends on the persistence methods. Base the choice on how far the domain is likely to diverge from its tables.

_Usage:_

"Why did the backfill email every customer?"

"`User` has an `afterSave` hook that sends the notification. Run the backfill with callbacks skipped, then move that email into the signup use case."

### Data mapper

A data mapper is a layer that moves data between in-memory objects and a database while keeping the two independent of each other. The domain objects contain no SQL and do not know a database exists, and the schema does not need to match the object structure. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002). Hibernate, SQLAlchemy's ORM and Doctrine are widely used implementations.

```typescript
class OrderMapper {
  constructor(private db: Db) {}

  async findById(id: string): Promise<Order | null> {
    const row = await this.db.one("select * from orders where id = $1", [id]);
    return row ? new Order(row.id, Money.cents(row.total_cents), row.status) : null;
  }

  async update(order: Order) {
    await this.db.none("update orders set status = $1 where id = $2", [
      order.status,
      order.id,
    ]);
  }
}
```

The pattern addresses the mismatch between object and relational structure. A `Customer` may hold an `Address` [value object](#value-object) and a list of preferences, while the database stores them across three tables with legacy column names. With [active record](#active-record), the object has to mirror those tables, so a schema change reaches business code. With a mapper, only the mapping changes, and the [domain model](#domain-model) can be tested without a database. Teams often notice the need when a column rename touches dozens of business files, or when a unit test for a pricing rule requires a running Postgres instance.

The costs are extra code and indirection. Each field is named in the object, the mapping and the schema, so a new column needs changes in all three. Mapping libraries remove some of this work but add configuration and behaviour of their own. For tables that map one to one onto simple objects, a mapper has little to separate, and active record is usually simpler.

Mapping libraries commonly combine a data mapper with a [unit of work](#unit-of-work) to batch writes and an [identity map](#identity-map) to avoid duplicate instances of a row.

A data mapper is often confused with the repository pattern. The mapper deals in rows and fields and knows the schema. A repository sits above it, exposing a collection-like interface in domain terms such as `findOverdue()`, and uses a mapper for the translation. In small codebases, one class may perform both roles.

_Usage:_

"Renaming `cust_ref` touched thirty files."

"Those files read row fields directly. Put a data mapper in front of the table so the next rename lives in one place."

### Unit of work

A unit of work is an object that tracks the changes made during a business operation and writes them to the database together, as one commit. Code loads and modifies objects in memory, and the unit of work determines which inserts, updates and deletes are needed. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002). Hibernate's `Session`, Entity Framework's `DbContext` and SQLAlchemy's `Session` are implementations.

```typescript
async function payOrder(uow: UnitOfWork, orderId: OrderId, payment: Payment) {
  const order = await uow.orders.get(orderId);
  order.markPaid(payment);
  uow.ledger.add(LedgerEntry.forPayment(order, payment));
  await uow.commit();
}
```

The pattern prevents operations that half-succeed. If `orders.save()` and `ledger.save()` each commit on their own, a crash between them leaves an order marked as paid with no ledger entry, and the data stays wrong until a reconciliation finds it. With a unit of work, both changes commit or neither does.

| Step    | Who                                    | What happens                                     |
| ------- | -------------------------------------- | ------------------------------------------------ |
| Begin   | [Service layer](#service-layer)  | Opens a unit of work for the use case            |
| Load    | Repositories or mappers                | Read objects and register them as tracked        |
| Change  | Domain objects                         | Modify state in memory                           |
| Commit  | Unit of work                           | Computes the changes, writes in one transaction  |
| Failure | Unit of work                           | Rolls back and discards tracked state            |

Deferring writes until commit causes some surprises. A query issued mid-operation may not see pending changes unless the library flushes first, and constraint violations appear at commit, far from the line that caused them. A unit of work also cannot cover external effects. An email sent before commit still goes out if the commit fails, so send it afterwards or record it with the outbox pattern.

A unit of work differs from a database transaction. The transaction is the storage guarantee, while the unit of work is the application-level object that collects changes and applies them in one at commit. Keep it scoped to one request or job, because a long-lived one accumulates tracked objects and stale state. It often uses an [identity map](#identity-map) so that each row is tracked once.

For a single-table update, a plain database transaction is enough.

_Usage:_

"We have paid orders with no ledger entries."

"Each repository commits separately. Wrap the payment in one unit of work so both writes succeed or fail together."

### Identity map

An identity map is a registry that records every object loaded during a session, keyed by its database identity, so the same row always resolves to the same in-memory object. Before loading a row, the data access code checks the map and returns the existing instance if there is one. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002).

```typescript
class IdentityMap<T> {
  private items = new Map<string, T>();

  get(id: string) {
    return this.items.get(id);
  }

  add(id: string, item: T) {
    this.items.set(id, item);
  }
}

async function findUser(map: IdentityMap<User>, mapper: UserMapper, id: string) {
  const known = map.get(id);
  if (known) return known;

  const user = await mapper.load(id);
  map.add(id, user);
  return user;
}
```

The pattern prevents two copies of one row from diverging within a single request. Without it, one function loads customer 42 and changes the email, another loads customer 42 and changes the plan, and whichever saves last overwrites the other's change. The result is a lost update with no error. With a map, both functions hold the same object, and both changes are saved.

An identity map usually lives inside a [unit of work](#unit-of-work), and [data mapper](#data-mapper) libraries such as Hibernate and SQLAlchemy provide one in their sessions. It should last only as long as that session. A process-wide map keeps objects alive indefinitely, serves stale data, and can expose one user's data to another request.

The main surprise is stale reads within a session. If a raw SQL statement or another process updates a row, loading it again through the session may return the object with its old field values, because the existing instance takes precedence. The fix is an explicit refresh, or ending the session before re-reading.

An identity map differs from a cache. A cache exists to avoid work, may be shared across requests and needs an expiry policy. An identity map exists to guarantee one object per row inside a session. It can save a query when loading by primary key, but a query on other criteria still goes to the database and then resolves the returned rows to existing instances.

_Usage:_

"The test updates the row with raw SQL, but `findById` still returns the old status."

"The session's identity map is handing back the loaded instance. Refresh it or read through a new session."

### Lazy load

Lazy load is a pattern in which an object defers loading related data until code first accesses it. A `Customer` can be fetched without its orders, and the orders are queried only when something asks for them. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002), and most ORMs offer it as an option or a default.

```typescript
class Customer {
  private orders?: Order[];

  constructor(
    readonly id: string,
    private loadOrders: (id: string) => Promise<Order[]>,
  ) {}

  async getOrders() {
    this.orders ??= await this.loadOrders(this.id);
    return this.orders;
  }
}
```

The pattern avoids loading data that a use case never reads. Fetching a customer to show a name should not pull thousands of order rows. Fowler describes four forms:

| Form                | How it works                                                  |
| ------------------- | ------------------------------------------------------------- |
| Lazy initialisation | A field starts empty and is loaded on first access            |
| Virtual proxy       | A [proxy](#proxy-pattern) stands in and loads when used |
| Value holder        | A wrapper object loads the value when asked                   |
| Ghost               | A partial object loads its remaining fields on first access   |

The best-known failure is the N+1 query problem. A list page loads 50 orders, then a template reads `order.customer.name` for each one, issuing one query per row. The page is quick in development with five rows and slow in production, and nothing in the template looks like a database call. This makes lazy loading a [leaky abstraction](#leaky-abstraction), because a property access can carry a network round trip.

A related failure occurs after the session closes. In Hibernate, touching an unloaded relation outside its session throws `LazyInitializationException`, often in a view or serialiser far from the original query.

To use it safely, fetch what a use case needs up front with a join or batch query, and keep laziness for data that is rarely read. Log query counts per request in development so N+1 patterns appear before release. Lazy load differs from pagination and caching: it changes when data is fetched, while pagination limits how much is fetched and caching avoids fetching it again.

_Usage:_

"The orders page makes 340 queries."

"Each row lazily loads its customer. Fetch the customers in one batch with the list query."

### Data transfer object

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

A DTO separates what a system exposes from how it stores data. Serialising a database [entity](#entity) directly is a common source of incidents: a new `passwordHash` column appears in a JSON response, or a column rename breaks a mobile client that still expects the old field. With a DTO, each exposed field is listed deliberately, and the internal model can change while the contract stays stable.

A request DTO also marks where untrusted input is validated. Parsing the request into a typed shape with a schema library prevents mass assignment, where a client sets a field such as `isAdmin` because the handler passed the entire body to the database.

| Type                                | Has behaviour | Identity              | Purpose                            |
| ----------------------------------- | ------------- | --------------------- | ---------------------------------- |
| DTO                                 | No            | No                    | Carries data across a boundary     |
| [Value object](#value-object) | Yes           | No, compared by value | Models a domain concept            |
| Entity                              | Yes           | Yes                   | Models something tracked over time |

DTOs cost mapping code, and each new field is touched in several places. For an internal tool where one team owns the API and the table and changes them together, separate DTOs may add boilerplate with little protection. Where an API has external consumers, the separation is usually worth it. Keep rules out of DTOs, because pricing logic placed on a response type is invisible to anyone reading the [domain model](#domain-model).

_Usage:_

"Why is `passwordHash` in the profile response?"

"The handler serialises the user row. Return a `UserResponse` DTO that lists only the public fields."

### Gateway pattern

The gateway pattern wraps access to an external system or resource in an object whose interface is owned by the application. Code calls `payments.charge(amount, token)` instead of using a vendor SDK or building HTTP requests. Martin Fowler catalogued the pattern in Patterns of Enterprise Application Architecture (2002).

```typescript
interface PaymentGateway {
  charge(amount: Money, token: string): Promise<ChargeResult>;
}

class StripeGateway implements PaymentGateway {
  constructor(private stripe: Stripe) {}

  async charge(amount: Money, token: string) {
    const intent = await this.stripe.paymentIntents.create({
      amount: amount.cents,
      currency: amount.currency,
      payment_method: token,
      confirm: true,
    });
    return { id: intent.id, succeeded: intent.status === "succeeded" };
  }
}
```

The pattern addresses external details spreading across a codebase. When a payment SDK is imported in forty files, a major version upgrade touches all of them, changing vendor becomes a project, and every test that reaches that code needs network access or an elaborate mock. With a gateway, the SDK appears in one class. Tests substitute an in-memory implementation at this [seam](#seam), and retries, timeouts and error translation have one home.

A useful gateway interface uses the application's vocabulary and returns its types. If `charge` returns a raw Stripe object, callers still depend on Stripe, which makes the wrapper a [leaky abstraction](#leaky-abstraction). Translate vendor errors into a small set of meaningful failures, such as `CardDeclined`.

| Pattern                                              | Purpose                                 | Scope                |
| ---------------------------------------------------- | --------------------------------------- | -------------------- |
| Gateway                                              | Wraps access to an external system      | One outside resource |
| [Adapter](#adapter-pattern)                    | Converts one interface to another       | Any two interfaces   |
| [Facade](#facade-pattern)                      | Simplifies a complicated subsystem      | Often internal       |
| [Anti-corruption layer](#anti-corruption-layer) | Protects a model from a foreign one     | A whole integration  |

The name overlaps with API gateway, a separate piece of infrastructure that routes network requests to backend services. A gateway in this sense is an in-process class. It is also commonly implemented with an adapter, so both labels can apply to the same code. Skip the wrapper for stable platform features that tests have no need to replace, such as a standard-library function.

_Usage:_

"Upgrading the Stripe SDK changed 38 files."

"Every feature calls it directly. Add a `PaymentGateway` and move the SDK behind it as part of this upgrade."

### Specification pattern

The specification pattern represents a business rule as an object that answers whether a candidate satisfies it. Specifications can be combined with `and`, `or` and `not` to build larger rules from small named ones. Eric Evans and Martin Fowler described the pattern, and Evans includes it in Domain-Driven Design (2003).

```typescript
interface Specification<T> {
  isSatisfiedBy(candidate: T): boolean;
}

const and = <T>(a: Specification<T>, b: Specification<T>): Specification<T> => ({
  isSatisfiedBy: (c) => a.isSatisfiedBy(c) && b.isSatisfiedBy(c),
});

const isActive: Specification<Customer> = {
  isSatisfiedBy: (c) => c.status === "active",
};
const hasNoDebt: Specification<Customer> = {
  isSatisfiedBy: (c) => c.balance >= 0,
};
const canReorder = and(isActive, hasNoDebt);
```

The pattern addresses a rule written in several forms. The definition of a customer who can reorder may exist in a `WHERE` clause, a validation check and a UI condition. When the definition changes, one is missed, and the application offers a button that then fails at checkout. A specification gives the rule one name and one definition. Evans lists three uses: validating an object, selecting matching objects from a collection, and describing what something to be created must satisfy.

The main difficulty is the database. An `isSatisfiedBy` function runs in memory, so using it for selection means loading every row and filtering in the application, which passes in tests and times out on a production table. One solution is for each specification to also produce a query expression, which adds a small [interpreter](#interpreter-pattern) to the codebase and needs tests to keep the two forms consistent. Another is to build specifications on an ORM's query objects, which ties them to that ORM.

The pattern is unnecessary for most conditions. A named predicate such as `canReorder(customer)` provides one definition with far less machinery, and it is enough until rules must be combined at runtime or stored as configuration. Use the full pattern when the combinations themselves vary.

It differs from the [strategy pattern](#strategy-pattern). A strategy selects how to perform an operation, such as which pricing algorithm to run. A specification answers yes or no about a candidate. The two can work together, with a specification deciding which strategy applies.

_Usage:_

"The button says the customer can reorder, but checkout rejects them."

"The UI and checkout each have their own rule. Define `canReorder` once and have both call it."

### Plugin architecture

A plugin architecture is a structure in which a host application defines extension points, and separately packaged modules add behaviour by implementing them. The host does not know at compile time which plugins exist. It discovers or receives them through configuration and calls them at defined moments. VS Code extensions, ESLint rules and webpack plugins work this way.

```typescript
type BuildHook = (files: File[]) => File[];

interface Plugin {
  name: string;
  setup(host: { onBuild(hook: BuildHook): void }): void;
}

function loadPlugins(plugins: Plugin[]) {
  const hooks: BuildHook[] = [];
  for (const plugin of plugins) {
    plugin.setup({ onBuild: (hook) => hooks.push(hook) });
  }
  return (files: File[]) => hooks.reduce((acc, hook) => hook(acc), files);
}
```

The pattern addresses features that vary by customer, environment or community. Without it, the main codebase fills with branches such as `if (customer === "acme")`, and each new integration requires a change and a release of the host. With extension points, new behaviour ships as a new module, which applies the [open-closed principle](#open-closed-principle) at application level. The host calls the plugin, a form of [inversion of control](#inversion-of-control).

The plugin API becomes a public contract, and this is the main cost. Hooks, arguments and lifecycle details that plugins rely on are hard to change, and a host upgrade that alters them breaks plugins the team has never seen.

| Concern           | Failure                                  | Mitigation                                |
| ----------------- | ---------------------------------------- | ----------------------------------------- |
| Versioning        | An upgrade breaks installed plugins      | Version the API and declare compatibility |
| Ordering          | Plugins conflict depending on load order | Define explicit phases                    |
| Failure isolation | One plugin crashes the host              | Catch errors or use a separate process    |
| Security          | Third-party code has host permissions    | Sandbox or restrict capabilities          |
| Performance       | Slow plugins delay startup               | Load on demand and measure                |

Avoid this structure when the variation is hypothetical. Building extension points before a second implementation exists is [speculative generality](#speculative-generality), and the resulting API is likely to be wrong. Extract extension points from real cases.

A plugin architecture differs from [microkernel architecture](#microkernel-architecture). In a microkernel, the host is a minimal system and most functionality, including essential features, is delivered as plugins. A plugin architecture can also describe a complete application with optional extensions.

_Usage:_

"Another customer wants a custom export format."

"Stop adding branches to the exporter. Define an export hook and ship this format as a plugin."

### Front controller

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

Most web frameworks apply the pattern implicitly. An Express or Fastify application is a front controller with a router, and its middleware pipeline is a form of [chain of responsibility](#chain-of-responsibility). The front controller usually dispatches to [model-view-controller](#model-view-controller) controllers, which handle individual actions.

| Approach         | Entry point              | Cross-cutting logic         | Fits                       |
| ---------------- | ------------------------ | --------------------------- | -------------------------- |
| Page controller  | One per page or endpoint | Repeated or inherited       | Few, independent pages     |
| Front controller | One per application      | Applied centrally           | Most web applications      |
| API gateway      | One for many services    | Applied at the network edge | Multiple deployed services |

Centralisation has trade-offs. A bug in the dispatcher affects every route, and shared steps add latency to endpoints that do not need them, such as health checks. Limit the controller to routing and cross-cutting work, because once it holds business rules or per-route conditionals, it starts to become a [god object](#god-object). Make authorisation deny by default, so that a route missing its configuration fails closed.

The pattern fits less well on platforms that deploy each function separately, since each function has its own entry point. There, shared logic usually moves into a wrapper function applied to each handler.

_Usage:_

"The new reports endpoint was reachable without logging in."

"Auth is applied per route. Move it into the front controller and make public routes opt out."

### Model-view-controller

Model-view-controller, or MVC, is a pattern that divides a user interface into three roles: the model holds data and rules, the view displays it, and the controller handles input. Trygve Reenskaug devised it for Smalltalk at Xerox PARC in the late 1970s. The aim was to let the same data be displayed in several ways and to keep presentation code apart from application logic, an early form of [separation of concerns](#separation-of-concerns).

| Role       | Responsibility                    | Should not                  |
| ---------- | --------------------------------- | --------------------------- |
| Model      | Holds state and business rules    | Know how it is displayed    |
| View       | Renders the model                 | Contain business rules      |
| Controller | Translates input into model calls | Hold business logic         |

The name now describes two different designs. In the original desktop form, views subscribed to the model through the [observer pattern](#observer-pattern), so a model change updated every view. In server-side web frameworks such as Rails and Spring MVC, a controller handles an HTTP request, loads data and renders a template once, with no ongoing observation. Many disagreements about what MVC means come from mixing these two.

```typescript
class ArticlesController {
  constructor(private articles: ArticleStore, private view: ArticleView) {}

  async show(req: AppRequest) {
    const article = await this.articles.get(req.params.id);
    return article ? this.view.render(article) : notFound();
  }
}
```

The most frequent failure is the fat controller. Validation, pricing and email sending accumulate in action methods because the controller is the first place a developer can reach, and the same logic must then be copied to the API or a background job. Move that work to a [service layer](#service-layer) or onto domain objects, and leave the controller to parse input and choose a response.

MVC is a presentation pattern and does not describe a full application. A codebase with `models/`, `views/` and `controllers/` folders can still have no clear structure in its business logic. The related [model-view-presenter](#model-view-presenter) and [model-view-viewmodel](#model-view-viewmodel) patterns change how the view and the logic communicate, mainly to make UI logic easier to test.

_Usage:_

"The checkout action is 400 lines, and the mobile API has a copy of it."

"Extract the logic into a service so both controllers only handle input and output."

### Model-view-presenter

Model-view-presenter, or MVP, is a user interface pattern in which a presenter holds the presentation logic and communicates with a view through an interface. The view forwards user actions to the presenter and displays what it is told. The model holds data and business rules, and the view does not access it directly. The pattern emerged in the 1990s and became common in Windows Forms and Android applications.

```typescript
interface LoginView {
  showError(message: string): void;
  goToDashboard(): void;
}

class LoginPresenter {
  constructor(private view: LoginView, private auth: Auth) {}

  async submit(email: string, password: string) {
    const ok = await this.auth.signIn(email, password);
    if (ok) this.view.goToDashboard();
    else this.view.showError("Incorrect email or password");
  }
}
```

The pattern addresses UI logic that can only be tested through the UI. When a screen's rules live in an Android `Activity` or a form class, checking that a failed login shows an error requires launching the screen, and such tests are slow and flaky. With a presenter, a test passes a fake `LoginView` and asserts that `showError` was called, with no rendering involved.

MVP differs from its neighbours in how the view receives updates:

| Pattern                                             | Who handles input          | How the view updates         | View knows about |
| --------------------------------------------------- | -------------------------- | ---------------------------- | ---------------- |
| [MVC](#model-view-controller)                   | Controller                 | Observes or is rendered      | Model            |
| MVP                                                 | View forwards to presenter | Presenter calls view methods | Presenter        |
| [MVVM](#model-view-viewmodel)                   | View binds to commands     | Data binding to state        | Viewmodel        |

Martin Fowler separated two variants. In Passive View, the presenter sets every field, so the view contains almost no logic. In Supervising Controller, the view handles simple data binding and the presenter handles the complicated cases.

The main costs are boilerplate and presenter size. Each screen needs a view interface and manual update calls, and one forgotten call leaves the screen out of sync with its state. Presenters can also grow into [god objects](#god-object) on complicated screens, so split them by component. In frameworks with reactive binding, MVVM or plain components usually need less code, and MVP is mostly seen in existing codebases.

_Usage:_

"Testing the login error means booting an emulator."

"Move the logic to a presenter behind a `LoginView` interface, then test it with a fake view."

### Model-view-viewmodel

Model-view-viewmodel, or MVVM, is a user interface pattern in which a viewmodel exposes a screen's state and commands, and the view binds to them declaratively. When the state changes, the binding updates the view, and the viewmodel holds no reference to the view. The pattern came from Microsoft's work on WPF in the mid-2000s and builds on Martin Fowler's Presentation Model.

```typescript
class CartViewModel {
  items = signal<CartItem[]>([]);
  total = computed(() => sum(this.items().map((item) => item.price)));
  canCheckout = computed(() => this.items().length > 0);

  remove(id: string) {
    this.items.update((list) => list.filter((item) => item.id !== id));
  }
}
```

The pattern removes manual UI update code. In [model-view-presenter](#model-view-presenter), each state change needs a call such as `view.showTotal()`, and a forgotten call leaves a stale total. In MVVM, `total` is derived state, so the display follows it. Because the viewmodel has no UI dependency, a test can call `remove()` and assert on `total` without rendering anything.

| Layer     | Holds                                  | Knows about          |
| --------- | -------------------------------------- | -------------------- |
| Model     | Data and business rules                | Neither of the others |
| Viewmodel | Screen state, derived values, commands | The model            |
| View      | Markup and bindings                    | The viewmodel        |

The pattern is common in WPF, in Android with Jetpack's `ViewModel`, and in SwiftUI, and Vue's design was partly inspired by it.

Its failures are harder to trace than explicit calls. Bindings can fail quietly, so a misspelled property in WPF leaves a blank field with no exception, and chains of derived state can trigger update loops or redundant renders. Viewmodels also grow into [god objects](#god-object) when one is created per page and handles every widget on it. Split them by component and keep business rules in the model, since a viewmodel only decides how data is presented.

MVVM differs from [model-view-controller](#model-view-controller), where a controller receives input and selects what to render. In MVVM, input reaches commands through bindings, and rendering follows state. For a small screen or a server-rendered page, a viewmodel is an extra layer with little to test. Many component frameworks already combine these roles using hooks or signals, and a separate class is only needed when the logic is large enough to test alone.

_Usage:_

"The cart total stays stale after removing an item."

"Someone set it by hand in the click handler. Make it a computed value on the viewmodel."

## Section 7 — Domain Modelling

### Ubiquitous language

A ubiquitous language is a shared vocabulary that developers and domain experts use for a business domain, in conversation, in documents and in the code itself. Eric Evans introduced the term in Domain-Driven Design (2003). If the business says a policy is "renewed", the code has a `renew()` method and not `updateStatus(3)`.

The practice addresses translation between business and engineering. When sales says "account" for a company, support says "account" for a login, and the code calls both `User`, every conversation needs interpretation, and a ticket can be built correctly against the wrong meaning. The mismatch is often found late, when a feature ships and the stakeholder says it is not what they asked for.

| Business says       | Code without a shared language | Code with one             |
| ------------------- | ------------------------------ | ------------------------- |
| Renew a policy      | `updateStatus(policy, 3)`      | `policy.renew()`          |
| Member has lapsed   | `user.flag === false`          | `member.hasLapsed()`      |
| Item is back-ordered | `item.qty < 0`                | `item.isBackOrdered()`    |

A ubiquitous language applies within one bounded context and is not a company-wide glossary. "Customer" can legitimately mean different things in billing and in shipping, and forcing one definition produces a bloated model that fits neither. A [context map](#context-map) records where meanings change and how terms translate between contexts.

Maintaining the language takes ongoing work. Keep a short glossary in the repository, using the words domain experts use. When a discussion changes the meaning of a term, rename the class, the method and the database column as part of the same work, or the code and the conversation drift apart. If a concept is hard to name, raise it with the experts as a modelling question, since the difficulty often means the concept is not yet understood.

The vocabulary feeds the [domain model](#domain-model), where each important term has a corresponding type or method. A developer reading the code and an expert describing the process should then be using the same words for the same things.

_Usage:_

"Is a member the person paying or the person on the plan?"

"Ask support, then use their word everywhere. Right now the code calls both `user`."

### Context map

A context map is a document or diagram that shows the bounded contexts in a system and the relationships between them. Eric Evans introduced it in Domain-Driven Design (2003). Each relationship records which side depends on which, how their models translate, and how the teams coordinate.

The map makes hidden dependencies visible. Without one, a team renames a field in its event and learns from an incident that three other teams were consuming it. A context map shows who is upstream, whose changes flow to others, and who is downstream and absorbs them. It also shows where one word carries different meanings, so that each context keeps its own [ubiquitous language](#ubiquitous-language).

| Relationship                                          | Meaning                                               |
| ----------------------------------------------------- | ----------------------------------------------------- |
| Partnership                                           | Two teams plan and release dependent changes together |
| [Shared kernel](#shared-kernel)                 | Two contexts jointly own a small shared model         |
| Customer-supplier                                     | Upstream includes downstream's needs in its planning  |
| Conformist                                            | Downstream adopts upstream's model as it is           |
| [Anti-corruption layer](#anti-corruption-layer) | Downstream translates upstream's model into its own   |
| Open host service                                     | Upstream offers a defined protocol for many consumers |
| Published language                                    | Contexts exchange data in a documented shared format  |
| Separate ways                                         | Contexts do not integrate                             |

A map should describe the current situation, including the awkward parts. Drawing the intended architecture hides the problems the exercise is meant to find. If billing is in practice conformist to a vendor's data model, record that, because it shows where a vendor change will land.

The relationships are organisational as well as technical. A customer-supplier arrangement fails if the upstream team has no incentive to serve the downstream team, and [Conway's law](#conways-law) means team boundaries tend to appear in the integration structure. [Team Topologies](#team-topologies) offers a related vocabulary for how teams interact.

A context map differs from a container diagram in the [C4 model](#c4-model). The C4 diagram shows deployable units and how they communicate. A context map shows model boundaries and team relationships, and one context may span several deployed services. Update it when integrations change.

_Usage:_

"Who consumes the `CustomerUpdated` event?"

"Nobody knows, which is why the last rename broke fulfilment. Let's draw a context map before changing it."

### Subdomain

A subdomain is a distinct area of a business's overall activity, such as pricing, billing, shipping or identity. The term comes from Eric Evans's Domain-Driven Design (2003), and it describes the business itself and not the software. An online retailer has these areas whether it runs one application or fifty.

Subdomains are usually classified into three types:

| Type                          | Description                                     | Typical approach             | Retailer example  |
| ----------------------------- | ----------------------------------------------- | ---------------------------- | ----------------- |
| [Core](#core-domain)    | Differentiates the business                     | Build in-house, model richly | Pricing           |
| Supporting                    | Specific to the business but not differentiating | Build simply or outsource   | Returns handling  |
| Generic                       | The same problem in most businesses             | Buy or use open source       | Payments, email   |

The classification guides where to spend engineering effort. Without it, teams apply the same level of design everywhere, so an internal admin screen receives an elaborate model while the rules that earn revenue sit in an untested script. Classifying subdomains makes that imbalance visible and supports decisions about what to build, buy or keep simple. A generic subdomain is often best served by a vendor behind a [gateway](#gateway-pattern).

The type depends on the business. Payments is generic for a bookshop and a core domain for a payments company. Classification also changes over time, as a capability that once differentiated a company becomes a commodity available from vendors.

A subdomain differs from a bounded context. The subdomain belongs to the problem space and describes what the business does. A bounded context belongs to the solution space and marks a boundary within which one model and its [ubiquitous language](#ubiquitous-language) apply. Aligning them one to one is a reasonable starting point, but legacy systems often have one context covering several subdomains, and a large subdomain may be split across contexts.

Identify subdomains by asking domain experts what the business does and where the work differs. The existing module structure is a weak guide, because it may reflect history or team layout, as [Conway's law](#conways-law) predicts.

_Usage:_

"Should we write our own invoicing engine?"

"Invoicing is a generic subdomain for us. Buy one and keep our engineers on pricing."

### Core domain

A core domain is the part of a business that differentiates it from competitors and that it must do well to succeed. For a logistics company it might be route optimisation, and for an insurer it might be risk pricing. Eric Evans defined the term as part of strategic design in Domain-Driven Design (2003). It is one of three types of [subdomain](#subdomain), alongside supporting and generic.

Identifying a core domain directs limited engineering effort. Without that decision, effort tends to follow technical interest: senior engineers build an in-house authentication system or workflow engine, while the pricing rules that win customers stay in an unowned script that nobody wants to change. The result is polished code in areas a vendor could have supplied and fragile code in the area that decides revenue.

The term is easily confused with "important". Payroll is essential and a failure would be serious, but it rarely distinguishes one company from another, so it is usually generic and bought. The test is whether doing it better than competitors would win business.

| Question                                    | If yes                        | If no                          |
| ------------------------------------------- | ----------------------------- | ------------------------------ |
| Would doing this better win customers?      | Candidate for a core domain   | Supporting or generic          |
| Could a vendor supply it equally well?      | Buy it                        | Consider building it           |
| Do its rules change with business strategy? | Keep in-house, model carefully | A simple implementation may do |

A core domain justifies investment that other areas do not: a rich [domain model](#domain-model), close work with domain experts, a precise [ubiquitous language](#ubiquitous-language) and experienced engineers. Protect it from vendor and legacy models with an [anti-corruption layer](#anti-corruption-layer), so that outside concepts do not shape its design.

Keep the list short, since a company that labels everything as core has made no decision. The classification can also change. A capability that once set a company apart may become a commodity, at which point it should be simplified or replaced with a product.

_Usage:_

"Should we spend next quarter rebuilding the notification service?"

"Notifications are generic for us. Use a vendor and put that time into the pricing engine, which is our core domain."

### Shared kernel

A shared kernel is a small part of a [domain model](#domain-model) that two bounded contexts explicitly share and jointly own. Neither team can change it without agreeing with the other. Eric Evans described it in Domain-Driven Design (2003) as one of the relationships recorded on a [context map](#context-map).

```typescript
// packages/billing-shipping-kernel/index.ts
export type OrderId = string & { readonly brand: "OrderId" };
export type Money = { cents: number; currency: "EUR" | "USD" };
```

The pattern addresses concepts that must stay identical on both sides. If billing and shipping each define `Money` or `OrderId` and the definitions diverge, values passed between them can be silently misread. Sharing a small package keeps the definition in one place, and the compiler catches disagreements.

The cost is [coupling](#coupling) between the two teams. Every change requires coordination, and both contexts must build and test against it before it merges. The usual failure is growth. A package named `common` starts with two types and collects customer logic because that is convenient, until a change for one team breaks another team's deployment. At that stage, teams wait on each other's releases, which is one route to a [distributed monolith](#distributed-monolith).

| Relationship                                          | Who owns the model | Coordination | Use when                                |
| ----------------------------------------------------- | ------------------ | ------------ | --------------------------------------- |
| Shared kernel                                         | Both teams jointly | High         | Teams work closely, concept is identical |
| Customer-supplier                                     | Upstream team      | Medium       | One team depends on another             |
| [Anti-corruption layer](#anti-corruption-layer) | Each side          | Low          | The models differ                       |
| Separate copies                                       | Each side          | None         | The concepts may diverge                |

A shared kernel differs from a general utility library. A utility library has no domain meaning and holds things like string helpers and date formatting. A shared kernel holds business concepts. It also differs from applying [DRY](#dry) across contexts: two definitions that look alike may represent different business concepts, and merging them ties together things that should change independently.

Keep the kernel small, give it tests that both teams run in CI, and require a review from each team on changes. If the teams stop coordinating or move to different release cycles, dissolve it and have each context own its copy.

_Usage:_

"Shipping's change to `common` broke our billing deploy again."

"That package has become a shared kernel nobody agreed to. Cut it down to `Money` and `OrderId` and move the rest back."

### Anti-corruption layer

An anti-corruption layer is a translation boundary that stops the model of an external or legacy system from spreading into a domain's own model. Code on the inside works only with its own concepts, and the layer converts to and from the foreign representation. Eric Evans described it in Domain-Driven Design (2003).

```typescript
type LegacyCustomer = { CUST_NO: string; STAT_CD: "A" | "S" | "X" };

const statuses = { A: "active", S: "suspended", X: "closed" } as const;

function toCustomer(raw: LegacyCustomer): Customer {
  return new Customer(CustomerId.of(raw.CUST_NO), statuses[raw.STAT_CD]);
}
```

The pattern addresses foreign concepts leaking into new code. A team rewrites a service, but because the data comes from a mainframe, the new classes contain fields like `STAT_CD`, the business logic branches on `"X"`, and every developer has to learn what the old codes mean. With a layer in place, the codes exist in one translation module, and the domain sees `suspended` and `closed`.

The layer usually combines a [facade](#facade-pattern) that simplifies the foreign API, [adapters](#adapter-pattern) that fit it to the interfaces the domain expects, and translators that convert data. It may also reconcile differences in behaviour, for example by combining three legacy calls into one domain operation.

| Option                     | Cost                         | Use when                                     |
| -------------------------- | ---------------------------- | -------------------------------------------- |
| Conform to upstream model  | Low now, [coupling](#coupling) later | The upstream model is good or the area is generic |
| Thin [gateway](#gateway-pattern) | Low              | Stable API, few concepts cross the boundary  |
| Anti-corruption layer      | Higher, with ongoing mapping | The foreign model is poor and the domain matters |

The layer is a maintenance cost, so apply it where the model matters. Protecting a [core domain](#core-domain) from a legacy schema usually justifies the effort. Wrapping a payment provider used in one generic flow usually does not. It is also a common companion to the strangler fig approach, where it lets new code run beside a legacy system during a migration.

An anti-corruption layer differs from a single adapter. An adapter fits one interface to another, often with one-to-one calls. An anti-corruption layer protects a model, and can contain substantial translation logic and many adapters.

_Usage:_

"Why does the new billing code check `STAT_CD === "X"`?"

"It reads the legacy record directly. Add an anti-corruption layer that maps those codes to our `AccountStatus`."

### Entity

An entity is a domain object defined by a stable identity and not by its attribute values. A customer who changes their name, email and address is still the same customer, because the identity persists through those changes. Eric Evans described entities in Domain-Driven Design (2003), alongside [value objects](#value-object), which have no identity.

```typescript
class Customer {
  constructor(readonly id: CustomerId, private email: Email) {}

  changeEmail(email: Email) {
    this.email = email;
  }

  equals(other: Customer) {
    return this.id === other.id;
  }
}
```

Identity determines equality. Two `Customer` objects with the same ID represent the same customer even if one has stale fields, and two customers named Sam Lee with different IDs are different people. A frequent bug comes from ignoring this: code compares objects with `===`, which checks the in-memory reference, so two loads of one customer appear unequal and a deduplication step keeps both. Comparing by ID fixes it, and an [identity map](#identity-map) can also ensure a single instance per session.

A good identity is generated once and never reused. Natural keys such as email addresses are risky because they change: a customer who updates their email either breaks every foreign key that references it or gets split into two records. Prefer a generated ID, and keep natural keys as unique attributes.

An entity has a lifecycle, and its methods should protect it. In place of public setters, expose operations such as `deactivate()` that check the [invariants](#invariant) for that transition. An entity with only getters and setters, whose rules live elsewhere, is part of an [anemic domain model](#anemic-domain-model).

The word has a narrower meaning in ORMs, where an entity is a class mapped to a table. A domain entity need not correspond to one table, and join tables and lookup rows are often not entities at all. To decide, ask whether the business tracks this thing individually over time. If two instances with the same values are interchangeable, model it as a value object. An entity may also sit inside an [aggregate](#aggregate), which controls changes to it.

_Usage:_

"The merge script kept both copies of the same customer."

"It compared objects by reference. Compare by customer ID, since that is what makes them the same entity."

### Value object

A value object is a domain object defined entirely by its attributes, with no identity of its own. Two `Money` objects of 10 euros are interchangeable, in the way that two ten-euro notes are for most purposes. Common examples are money, date ranges, addresses, coordinates and email addresses. Eric Evans described the pattern in Domain-Driven Design (2003).

```typescript
class Money {
  private constructor(readonly cents: number, readonly currency: string) {}

  static of(cents: number, currency: string) {
    if (!Number.isInteger(cents)) throw new Error("Cents must be an integer");
    return new Money(cents, currency);
  }

  add(other: Money) {
    if (other.currency !== this.currency) throw new Error("Currency mismatch");
    return new Money(this.cents + other.cents, this.currency);
  }

  equals(other: Money) {
    return this.cents === other.cents && this.currency === other.currency;
  }
}
```

Value objects address rules scattered around primitive fields. When money is a `number`, nothing stops code from adding euros to dollars, and floating-point arithmetic can leave an invoice one cent out. This is [primitive obsession](#primitive-obsession). A `Money` type puts the currency check and integer arithmetic in one place, and any instance that exists is valid because its constructor enforced the [invariants](#invariant).

Value objects are immutable, so an operation returns a new instance and leaves the original unchanged. This removes a class of aliasing bugs, such as two orders sharing one mutable `Address`, where editing one changes the other's delivery address.

| Property   | Value object         | [Entity](#entity)      |
| ---------- | -------------------- | -------------------------- |
| Defined by | Attributes           | Identity                   |
| Equality   | All attributes match | Same ID                    |
| Mutability | Immutable            | Changes over its lifecycle |
| Lifecycle  | Created and replaced | Tracked over time          |
| Example    | `Money`, `DateRange` | `Customer`, `Order`        |

The same concept can be either, depending on the domain. An address is a value object for an online shop, where only its contents matter, and may be an entity for a postal service that tracks each delivery point over time.

Value objects are usually stored as columns on the owning table or as a JSON field, without an ID of their own. They are unnecessary for a field with no rules, so introduce them where a value has validation, units or operations. A value object differs from a [data transfer object](#data-transfer-object), which only carries data across a boundary and enforces nothing.

_Usage:_

"The invoice total is off by a cent, and one line is in dollars."

"Prices are plain numbers. Introduce a `Money` value object that stores cents and rejects mixed currencies."

### Aggregate

An aggregate is a cluster of domain objects that is treated as one unit for changes, with a single root [entity](#entity) through which all modifications pass. An `Order` root might contain `OrderLine` objects, and code outside calls `order.addLine()` without ever editing a line directly. Eric Evans described the pattern in Domain-Driven Design (2003).

```typescript
class Order {
  private lines: OrderLine[] = [];

  constructor(
    readonly id: OrderId,
    readonly customerId: CustomerId,
    private limit: Money,
  ) {}

  addLine(product: ProductId, price: Money, quantity: number) {
    const line = new OrderLine(product, price, quantity);
    if (this.total().add(line.subtotal()).greaterThan(this.limit)) {
      throw new OrderLimitExceeded();
    }
    this.lines.push(line);
  }

  total() {
    return this.lines.reduce((sum, l) => sum.add(l.subtotal()), Money.zero("EUR"));
  }
}
```

The pattern protects rules that span several objects. Suppose an order may not exceed a credit limit. If two requests each insert a line, each can check the total, each can pass, and the order ends up over the limit. With an aggregate, the order's [invariants](#invariant) are checked in one place, and a version number on the root detects the concurrent edit.

| Rule                                   | Reason                         |
| -------------------------------------- | ------------------------------ |
| Access children only through the root  | Nothing can bypass the rules   |
| Reference other aggregates by ID       | Keeps object graphs small      |
| Change one aggregate per transaction by default | Limits locking and contention |
| Load and save the aggregate as a whole | Rules see the complete state   |

Size is the main design decision. A common mistake is to model a `Customer` aggregate containing all orders, addresses and tickets because the nouns are related. Loading it pulls thousands of rows, and unrelated updates fail with version conflicts. Draw the boundary around what must be consistent immediately. Anything else can be updated afterwards, often in response to a [domain event](#domain-event).

An aggregate differs from an ORM relationship graph, which lets code navigate between objects and save each independently. It also differs from the [composite pattern](#composite-pattern), which treats a tree of objects uniformly and says nothing about transactional consistency. For data with no multi-object rules, a plain entity or a [transaction script](#transaction-script) is enough.

_Usage:_

"Two people edited the same order and it went over the credit limit."

"Lines are saved independently. Make `Order` the aggregate root and check the limit in `addLine`."

### Domain event

A domain event is an immutable record of something meaningful that happened in a business domain, named in the past tense. Examples are `OrderPlaced`, `PaymentFailed` and `SubscriptionCancelled`. An [aggregate](#aggregate) typically records the event when its state changes, and other parts of the system react to it.

```typescript
type OrderPlaced = {
  type: "OrderPlaced";
  orderId: OrderId;
  customerId: CustomerId;
  total: Money;
  occurredAt: Date;
};
```

Domain events address workflows where one function must know every consequence of an action. A `placeOrder` function starts by saving the order, then gains calls to reserve stock, send an email, update analytics and award loyalty points. Each new requirement edits the same function, and an analytics timeout can fail the checkout. With an event, `placeOrder` records `OrderPlaced` and each reaction subscribes separately, similar to the [observer pattern](#observer-pattern) at the level of the business.

| Message           | Form                  | Meaning                            | Recipients     |
| ----------------- | --------------------- | ---------------------------------- | -------------- |
| Command           | Imperative, `PlaceOrder` | A request that can be rejected  | One handler    |
| Domain event      | Past, `OrderPlaced`   | A fact that has already happened   | Zero or more   |
| Integration event | Past, versioned       | A fact published to other contexts | Other services |

Domain events are usually internal to a bounded context, so their shape can change with the model. Publishing them unchanged to other teams turns internal structure into a public contract. Translate them to a stable integration event at the boundary.

Delivery introduces failure modes. If code commits the order and crashes before publishing, the event is lost and the stock is never reserved. The outbox pattern addresses this by writing the event in the same transaction as the state change. Handlers must also tolerate duplicates and out-of-order delivery when messages cross a broker.

Events make control flow harder to follow, because a reader of `placeOrder` cannot see what happens next. Reserve them for facts other parts of the system care about, since a simple two-step operation is clearer as a direct call. Domain events are also distinct from event sourcing, which stores events as the system of record. A system can use domain events with ordinary state tables.

_Usage:_

"An analytics timeout failed the checkout again."

"Checkout shouldn't know about analytics. Publish `OrderPlaced` and let analytics consume it separately."

### Domain service

A domain service is a stateless operation that expresses a business rule which does not naturally belong to a single [entity](#entity) or [value object](#value-object). Eric Evans described it in Domain-Driven Design (2003). It is named in business language and takes domain objects as arguments, such as `DiscountPolicy.priceFor(order, customer, promotions)`.

```typescript
class DiscountPolicy {
  priceFor(order: Order, customer: Customer, promotions: Promotion[]): Money {
    const best = promotions
      .filter((promotion) => promotion.appliesTo(order, customer))
      .map((promotion) => promotion.discountOn(order.total()))
      .reduce((a, b) => (a.greaterThan(b) ? a : b), Money.zero(order.currency));

    return order.total().subtract(best);
  }
}
```

The pattern addresses rules that make any host object awkward. A discount that depends on an order, a customer's tier and the active promotions could go on `Order`, but then `Order` must know about promotions and tiers. Signs of a misplaced method are a long parameter list of other objects, or a method that reads more from its arguments than from `this`, a smell known as [feature envy](#feature-envy). Moving the rule to a domain service keeps each object focused.

A domain service is easily confused with an application service in a [service layer](#service-layer):

| Aspect     | Domain service              | Application service                            |
| ---------- | --------------------------- | ---------------------------------------------- |
| Contains   | Business decisions          | Orchestration of a use case                    |
| Depends on | Domain objects              | Repositories, transactions, gateways           |
| Example    | Calculate the best discount | Load order, apply discount, commit, send email |
| Tested with | Plain objects              | Fakes or integration tests                     |

To tell them apart, ask whether a domain expert would recognise the operation and care about its rules. If so, it belongs in the domain. If it is about loading, saving or sending, it belongs in the application layer.

Overuse is the main risk. When teams place every rule in classes named `OrderManager` or `CustomerHelper`, the entities become data holders and the design turns into an [anemic domain model](#anemic-domain-model). Put behaviour on an entity or value object first, and use a domain service only when that would make the model worse. Some domain services need outside data, such as an exchange rate. Define an interface in the domain and implement it in infrastructure, following the [dependency inversion principle](#dependency-inversion-principle).

_Usage:_

"`Order` now imports `Promotion`, `CustomerTier` and `TaxTable`. Is that right?"

"No. Pricing spans all of them, so pull it into a `DiscountPolicy` domain service."

### Invariant

An invariant is a condition that must always be true for an object or system whenever its state can be observed. Examples are an order's total equalling the sum of its lines, an account balance staying above its overdraft limit, and a booking's end date falling after its start date.

Broken invariants appear as data that should be impossible. Support finds an order with no lines, a refund larger than the original payment, or a subscription that is both active and cancelled. Developers respond by adding defensive checks such as `if (order.lines.length === 0)` throughout the code, because they can no longer trust the data. The usual cause is that several code paths write the same state and one skips a rule.

Invariants differ from input validation. Validation checks whether a request is acceptable and can reject it with a message, such as a malformed email. An invariant describes what must hold for an object's state regardless of how the change was requested. Validation runs at the boundary, while the model enforces the invariant for every path, including imports, scripts and background jobs.

| Enforcement                  | Example                                     | Coverage                     |
| ---------------------------- | ------------------------------------------- | ---------------------------- |
| Type system                  | `NonEmptyArray<OrderLine>` rules out no lines | Compile time               |
| Constructor                  | `Money.of` rejects a fractional cent        | Every instance               |
| [Aggregate](#aggregate) root | `addLine` checks the credit limit       | Every change via the root    |
| Database constraint          | `CHECK (ends_at > starts_at)`, unique index | Every write, including raw SQL |
| Reconciliation job           | Nightly comparison of ledger and payments   | Detects violations afterwards |

Prefer the earliest level that can express the rule. Keep fields private so that [encapsulation](#encapsulation) stops code from bypassing the check, and add a database constraint for rules that must survive scripts and migrations.

Invariants that span several aggregates cannot normally be kept within one transaction. Such rules are usually relaxed to eventual consistency, with compensating actions or reconciliation. Ask the business how long a violation can be tolerated, because the answer often changes where the aggregate boundary is drawn.

_Usage:_

"How did a refund end up larger than the payment?"

"The admin script writes refunds directly. Put that invariant on `Payment.refund` and add a database constraint."

### Event storming

Event storming is a collaborative workshop in which developers and domain experts map a business process as a timeline of [domain events](#domain-event) on sticky notes. Alberto Brandolini created the technique. Participants work on a long wall or shared digital board, writing past-tense statements such as "Order placed" and "Payment failed".

The workshop addresses knowledge that is spread across people. Requirements documents often describe the intended process, each department knows only its own step, and contradictions surface after code is written. In a workshop, a warehouse lead can point out that "order shipped" happens twice for split deliveries, which nobody in engineering knew. Finding that on a wall takes minutes, while finding it in production can mean a data migration.

| Step                | Who         | What happens                                                                |
| ------------------- | ----------- | --------------------------------------------------------------------------- |
| Explore             | Everyone    | Write events on orange notes, without ordering them                         |
| Timeline            | Everyone    | Arrange events in order and merge duplicates                                |
| Hotspots            | Facilitator | Mark disagreements and unknowns in a contrasting colour                     |
| Commands and actors | Group       | Add what triggered each event and who did it                                |
| Policies            | Group       | Add rules of the form "whenever X happens, do Y"                            |
| Boundaries          | Group       | Group related events into candidate contexts and [aggregates](#aggregate) |

Brandolini describes formats at different levels of detail. A Big Picture session covers an entire business and looks for problems and opportunities. Process Modelling examines one process. Software Design goes further, towards aggregates and code.

Results depend on who attends. Without the people who do the work, the group documents its own assumptions and the session adds little. A facilitator keeps the discussion moving and records disputes as hotspots, so the group does not stop to resolve each one.

The output is a shared understanding plus inputs to design: a draft [ubiquitous language](#ubiquitous-language), candidate boundaries for a [context map](#context-map) and a list of open questions. It is not a finished design, and the wall should not be transcribed one to one into classes. For a small, well-understood feature, a conversation is enough.

_Usage:_

"Sales, ops and finance each describe refunds differently."

"Let's run an event storming session with all three and mark the disagreements as hotspots."

## Section 8 — Architecture Styles

### Clean architecture

Clean architecture organises a system into concentric rings in which source code dependencies point only inward. Robert C. Martin set it out in his 2017 book _Clean Architecture_. The inward-only constraint is called the dependency rule: an inner ring never names anything from an outer ring.

| Ring                   | Contains                                  | Example                                 |
| ---------------------- | ----------------------------------------- | --------------------------------------- |
| [Entities](#entity) | Enterprise-wide business rules            | `Invoice`                               |
| Use cases              | Application-specific workflows            | `ApproveInvoice`                        |
| Interface adapters     | Translation to and from external formats  | Controllers, presenters, store classes  |
| Frameworks and drivers | External tools                            | Web framework, ORM, database            |

It addresses business logic that cannot be tested or moved because it is entangled with a framework. A framework upgrade breaks pricing code, or a test of one discount calculation needs a running database. Under the dependency rule, the use case declares an interface and an outer ring implements it, which applies the [dependency inversion principle](#dependency-inversion-principle).

```typescript
// Use case ring: owns the interface
interface InvoiceStore {
  find(id: string): Promise<Invoice>;
  save(invoice: Invoice): Promise<void>;
}

class ApproveInvoice {
  constructor(private readonly invoices: InvoiceStore) {}

  async run(id: string): Promise<void> {
    const invoice = await this.invoices.find(id);
    invoice.approve();
    await this.invoices.save(invoice);
  }
}

// Adapter ring: depends inward
class PostgresInvoiceStore implements InvoiceStore {
  /* SQL here */
}
```

The structure has a cost. Adding one field to a screen can require changes to an entity, a use case's input and output models, a presenter and a mapper. For a CRUD application with little logic, those layers add translation without protecting anything, and a [transaction script](#transaction-script) or [vertical slice architecture](#vertical-slice-architecture) fits better. Apply the rings where business rules are complex and expected to outlive their delivery mechanism.

Clean architecture is often confused with hexagonal architecture and [onion architecture](#onion-architecture). All three keep domain code independent of infrastructure. Hexagonal architecture describes ports and adapters without prescribing inner layers, while onion and clean architecture name rings inside the application. The resulting code is often similar.

_Usage:_

"Testing the discount rule needs Postgres and a running web server."

"The rule is in the controller. Move it into a use case and give it a store interface."

### Onion architecture

Onion architecture arranges an application in concentric rings around its [domain model](#domain-model), with every dependency pointing toward the centre. Jeffrey Palermo named it in 2008 as an alternative to layered architecture, in which business code sits above and depends on the data access layer.

That dependency causes a recognisable problem. Replacing the ORM or changing a table forces edits to business classes, because those classes import data access types. A unit test for a pricing rule then needs a database.

| Ring                                     | Contains                                                                        | May depend on   |
| ---------------------------------------- | ------------------------------------------------------------------------------- | --------------- |
| Domain model                             | [Entities](#entity), [value objects](#value-object), business rules   | Nothing         |
| [Domain services](#domain-service) | Logic spanning several objects, repository interfaces                           | Domain model    |
| Application services                     | Use cases, transaction boundaries                                               | Both inner rings |
| Infrastructure and UI                    | Database code, HTTP, messaging, tests                                           | All inner rings |

The inner rings declare what they need as interfaces. The outer ring implements them and connects them at startup, usually through dependency injection.

```typescript
// Domain services ring
interface CustomerRepository {
  findById(id: CustomerId): Promise<Customer | null>;
}

// Infrastructure ring
class SqlCustomerRepository implements CustomerRepository {
  async findById(id: CustomerId) {
    /* query and map to a Customer */
    return null;
  }
}
```

The cost is indirection and mapping. Each external shape must be translated at the boundary, and a simple read may pass through several types that add nothing. Onion architecture suits long-lived systems with substantial business rules. For a small CRUD service, a [transaction script](#transaction-script) with direct queries is easier to maintain.

Onion architecture is most often confused with [clean architecture](#clean-architecture). Both enforce inward dependencies and keep frameworks at the edge. Onion places the domain model at the centre and emphasises where repository interfaces live, while clean architecture names an explicit use case ring and a ring of interface adapters. A team following either will produce similar code, so pick one vocabulary and use it consistently.

_Usage:_

"Why does the pricing class import our ORM's decorators?"

"It shouldn't. Move the mapping to infrastructure and keep a plain domain class in the centre."

### Vertical slice architecture

Vertical slice architecture organises code around individual features or requests rather than technical layers. Each slice contains what one operation needs: input validation, business logic, data access and response shape. Jimmy Bogard popularised the name.

It addresses changes that cut across every layer. Adding one field to an order screen in a layered codebase can mean editing a controller, a service, a repository, a [data transfer object](#data-transfer-object) and a mapper in five folders. Shared services also accumulate methods for unrelated callers, so a change made for one feature breaks another.

```text
features/
  place-order/
    handler.ts
    validate.ts
    place-order.test.ts
  cancel-order/
    handler.ts
    cancel-order.test.ts
```

Slices favour high [cohesion](#cohesion) within a feature and low [coupling](#coupling) between features. Each slice can choose its own approach: a simple read may run one SQL query, while a complex write may use a rich [domain model](#domain-model).

The main risk is duplication. Two slices may implement the same business rule and then diverge, for example when refund eligibility is checked differently in two features. Move a rule to shared domain code once it is a genuine business concept, rather than at the first sign of similar code. Vertical slices also fit poorly when many features must enforce the same complex [invariants](#invariant) over the same data, because those rules belong in a shared model.

Vertical slice architecture differs from [package by feature](#package-by-feature), which is a rule for arranging folders. A package-by-feature codebase can still repeat the same layers inside every folder. Vertical slice architecture goes further by treating each request as an independent unit with its own implementation and minimal sharing.

_Usage:_

"Adding a coupon field touched eleven files across six folders."

"Move checkout into one slice. The next field should change one folder."

### Pipes and filters

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

Pipes and filters is often confused with [chain of responsibility](#chain-of-responsibility). In a chain, each handler decides whether to handle a request or pass it on, and the request may stop early. In a pipeline, every filter normally processes each item and contributes to the transformed output.

_Usage:_

"The import fails somewhere in a 500-line function and we can't test any of it."

"Split it into parse, validate and load filters, then test each one with sample rows."

### Microkernel architecture

Microkernel architecture builds a system around a minimal kernel that provides only essential services, with other functionality delivered by plug-in modules. The term comes from operating systems such as Mach and MINIX, where services such as file systems run outside the kernel. At application level, the same structure appears in IDEs and in products extended per customer.

The style addresses a product whose variations have accumulated inside its main code. The symptom is branches such as `if (customer === "acme")` in billing logic, with each new client adding risk for all the others. A microkernel moves those variations behind a contract.

```typescript
interface Plugin {
  name: string;
  register(host: Host): void;
}

class Host {
  private handlers = new Map<string, (doc: Doc) => Doc>();

  addHandler(type: string, fn: (doc: Doc) => Doc) {
    this.handlers.set(type, fn);
  }

  load(plugins: Plugin[]) {
    for (const plugin of plugins) plugin.register(this);
  }
}
```

The kernel handles loading, the plug-in lifecycle and shared services such as configuration and logging. Plug-ins depend on the kernel's contract and ideally not on each other. That contract becomes a public API, so changing it can break every plug-in, including third-party ones. Version it and keep it small. A faulty plug-in can also crash the host unless it runs in a separate process or sandbox, which adds communication overhead.

Avoid the style when a product has few expected variations. Building an extension system for two known cases adds a contract to maintain and is a form of [speculative generality](#speculative-generality).

Microkernel architecture overlaps with [plugin architecture](#plugin-architecture), which describes the general technique of extending an application through plug-ins. A microkernel is the stricter form: the kernel is deliberately minimal, and much of the product's standard functionality is itself built as plug-ins. An application that accepts a few plug-ins around a large built-in feature set has a plugin architecture but not a microkernel.

_Usage:_

"Every new customer adds another branch to the billing code."

"Keep the billing engine small and ship each customer's rules as a plug-in."

### Service-oriented architecture

Service-oriented architecture (SOA) structures a system as a set of business capabilities exposed as network services with formal contracts. It became widespread in large enterprises in the 2000s, often using SOAP, WSDL and an enterprise service bus (ESB).

It addressed capabilities duplicated across departmental applications. When sales, billing and support each keep their own customer record, an address change reaches one and the others go stale. SOA places a capability such as customer lookup behind one service, so applications reuse it rather than reimplement it.

A typical enterprise deployment has three parts. Business services expose capabilities through published contracts. The ESB routes messages, transforms formats and connects older systems. A governance group approves contracts and manages reuse.

The ESB is where many SOA programmes ran into trouble. Routing rules, data transformations and business logic accumulate in the bus, so a small change requires a ticket to the integration team and a shared release. The bus becomes a delivery bottleneck and a shared point of failure. Heavy reuse also increases [coupling](#coupling), because a widely shared service cannot change without coordinating every consumer.

| Aspect            | Typical SOA               | Microservices                     |
| ----------------- | ------------------------- | --------------------------------- |
| Service scope     | Broad business capability | Narrow, independently deployable  |
| Data              | Often shared databases    | Owned per service                 |
| Integration logic | Central bus               | In the services, simple transport |
| Main goal         | Enterprise reuse          | Independent change and deployment |
| Governance        | Central                   | Mostly team-level                 |

Microservices are often described as a descendant of SOA, and the boundary between them is not sharp. SOA remains reasonable for integrating packaged products, such as ERP or CRM systems, that cannot be rewritten. Keep the bus limited to routing and protocol translation, and keep business rules inside the services. An [anti-corruption layer](#anti-corruption-layer) can protect newer code from a legacy contract.

_Usage:_

"Why does a new field on the customer API need the integration team?"

"The mapping lives in the ESB. Move it to the service and leave the bus doing routing only."

### Space-based architecture

Space-based architecture removes the database from the synchronous request path by processing transactions against replicated in-memory data. Application instances, called processing units, each hold the data they need, and changes are written to the database asynchronously. The name comes from the tuple space, a shared associative memory.

It addresses load that the database cannot absorb. During a ticket sale, web servers can be added in seconds, but requests still queue on a saturated database connection pool and the site times out. With the working data in memory, adding processing units adds both compute and data capacity.

| Component              | Role                                                     |
| ---------------------- | -------------------------------------------------------- |
| Processing unit        | Runs application code with an in-memory copy of its data |
| Data grid              | Replicates changes between processing units              |
| Messaging grid         | Routes incoming requests to available units              |
| Processing grid        | Coordinates requests that span several unit types        |
| Deployment manager     | Starts and stops units as load changes                   |
| Data pump              | Sends updates toward the database asynchronously         |
| Data writer and reader | Persist updates, and reload data after a restart         |

The trade-offs follow from asynchronous persistence. Updates accepted in memory can be lost if units fail before the pump delivers them. Two units can sell the same seat when replication lags, so conflicts need a resolution rule. Memory is costly, and realistic failure testing needs production-like load.

Use the style for spiky, high-volume workloads such as ticketing and auctions, where brief inconsistency can be reconciled. Avoid it for workloads that must enforce strict [invariants](#invariant) at commit, such as a ledger, for datasets too large to hold in memory, and for steady, moderate load.

Space-based architecture is often confused with adding a cache. A cache sits beside a database that remains the primary store for transactions, and writes normally still reach that database synchronously. In space-based architecture the grid is the working store for transactions, and the database is a durable copy that lags behind.

_Usage:_

"During on-sale the app servers idle while the database pool is exhausted."

"Caching reads won't fix the writes. We could hold seat inventory in a data grid and persist asynchronously."

### Blackboard pattern

The blackboard pattern lets several independent specialist components solve a problem by reading and updating a shared data structure, called the blackboard. A control component chooses which specialist runs next. The pattern originated in the Hearsay-II speech recognition system in the 1970s.

It addresses problems with no known fixed algorithm, where partial results from different kinds of expertise must be combined. In speech recognition, one specialist proposes sounds, another proposes words and another checks grammar. A fixed pipeline struggles here because a later insight may need to revise an earlier guess, which produces a tangle of special cases and backtracking.

| Part              | Responsibility                                              |
| ----------------- | ----------------------------------------------------------- |
| Blackboard        | Holds the problem, partial solutions and hypotheses         |
| Knowledge sources | Each applies one specialism and knows nothing of the others |
| Control           | Selects the next knowledge source from the board's state    |

```typescript
interface KnowledgeSource {
  canContribute(board: Board): boolean;
  contribute(board: Board): void;
}

function solve(board: Board, sources: KnowledgeSource[]) {
  while (!board.isSolved()) {
    const next = sources.find((s) => s.canContribute(board));
    if (!next) throw new Error("No source can make progress");
    next.contribute(board);
  }
  return board.solution();
}
```

Specialists can be added without changing each other, because they communicate only through the board. The costs are those of shared mutable state: the board's schema is a dependency of every specialist, concurrent updates need coordination, and results are hard to reproduce when execution order depends on the data. Termination also needs care, since two specialists can keep revising each other's work.

Do not use the pattern when a deterministic algorithm or a plain pipeline solves the problem. It suits work such as sensor fusion, planning and diagnosis, where the order of steps cannot be fixed in advance.

The blackboard pattern is often confused with the [observer pattern](#observer-pattern). An observer reacts to notifications from a subject and has no shared goal. A blackboard accumulates a partial solution, and a control strategy directs contributions toward completing it.

_Usage:_

"The fraud rules call each other in an order nobody can follow."

"Have each detector write its findings to a shared case record, and let one controller decide what runs next."

### Client-server architecture

Client-server architecture divides a system into clients, which initiate requests, and servers, which respond with data or perform work. A browser loading a page, a mobile app calling an API and an application connecting to a database are all client-server relationships. One program can play both roles: an API server is a server to its callers and a client of its database.

Centralising shared state and rules on the server makes them easier to update, secure and back up. Clients can be numerous and varied, because they only need to speak the protocol.

The split determines what each side can be trusted with. The server must treat all client input as untrusted, because a user can modify the client or call the API directly. A common failure is a discount or permission check performed only in the browser, which someone bypasses by replaying an edited request. Validate on the client for responsiveness and on the server for correctness.

| Variant        | Client does              | Server does             | Trade-off                               |
| -------------- | ------------------------ | ----------------------- | --------------------------------------- |
| Thin client    | Displays output          | Rendering and logic     | Simple to update, needs network         |
| Rich client    | UI logic and local state | Data and business rules | Responsive, more duplicated logic       |
| Offline client | Works on a local copy    | Synchronises changes    | Usable offline, needs conflict handling |

Clients and servers also change at different speeds. A web server deploys in minutes, while older mobile app versions may keep calling the API for years. Removing a response field can crash those versions even though all server tests pass, so API changes need to stay backward compatible or be versioned.

The server can become a bottleneck or single point of failure, which replication and load balancing address. [Peer-to-peer architecture](#peer-to-peer-architecture) removes the central role, at the cost of harder coordination and trust. Most product systems remain client-server because a central authority simplifies consistency, access control and operations.

_Usage:_

"Someone got a 100% discount by editing the checkout request."

"The limit is only enforced in the frontend. The server has to validate it too."

### Peer-to-peer architecture

Peer-to-peer (P2P) architecture connects nodes, called peers, that act as both client and server. Peers exchange data or work with each other rather than relying on a central server. Examples include BitTorrent for file distribution, Bitcoin for a shared ledger and WebRTC data channels for direct browser connections.

Capacity can grow with participation, because each peer that downloads a file can also upload it to others. No single server failure stops the network, and the operator's bandwidth costs can fall. In exchange, the system must solve problems that a central server handles implicitly: finding peers, agreeing on state and deciding whom to trust.

| Topology     | How peers are found                   | Trade-off                                     |
| ------------ | ------------------------------------- | --------------------------------------------- |
| Unstructured | Flooding or gossip between neighbours | Simple and resilient, lookups are inefficient |
| Structured   | Distributed hash table                | Efficient lookups, more upkeep during churn   |
| Hybrid       | Central tracker or signalling server  | Easy discovery, retains a central dependency  |

Network conditions are the first practical obstacle. A P2P feature often works between two machines on the same network and then fails between real users, because NAT on home routers and corporate firewalls blocks inbound connections. Applications use techniques such as STUN and hole punching, and fall back to a TURN relay when no direct path exists.

Peers also join and leave constantly, which is known as churn, so data must be replicated and no peer can be assumed to stay online. Peers cannot be trusted by default either. They may send corrupted data or create many fake identities to gain influence, which is called a Sybil attack. Content hashes, signatures and consensus protocols limit this.

Choose P2P when decentralisation, censorship resistance or distribution cost justifies the complexity. For most applications, [client-server architecture](#client-server-architecture) is simpler to secure, monitor and update, because it has one authority to operate.

_Usage:_

"Video calls work in the office but fail for half our customers."

"They're behind NAT. We need a TURN relay for when direct connections can't be established."

### Cell-based architecture

Cell-based architecture splits a system into multiple isolated units, called cells, each running a complete copy of the stack and serving a subset of customers. A thin routing layer sends each request to the customer's cell. Cells share as little as possible, including data stores.

The style limits blast radius, the share of customers affected by a failure. In a single shared deployment, one tenant's runaway query, a poison message or a bad configuration push can take down the service for everyone. With twenty equally sized cells, the same fault is normally contained to one cell, or five percent of customers.

| Part          | Role                                                       |
| ------------- | ---------------------------------------------------------- |
| Cell          | Independent full stack with its own compute and data       |
| Partition key | Value, often a tenant ID, that assigns a request to a cell |
| Cell router   | Maps a key to a cell and forwards the request              |
| Control plane | Creates cells, assigns tenants and moves them between cells |

Deployments roll out one cell at a time, so a faulty release can be caught before it reaches the whole fleet. Capacity grows by adding cells, and each cell has a known maximum size that can be load tested.

The router is shared by every request, so it must remain simple and highly available. Business logic placed there recreates the shared failure domain that cells were meant to remove. Other costs include running many copies of the infrastructure, moving tenants between cells, and building a separate path for cross-cell features such as global search or organisation-wide reports. Small systems rarely justify this overhead.

Cell-based architecture differs from two nearby techniques. Database sharding partitions only data, so a fault in a shared application tier still affects all shards. A bulkhead isolates resources inside a service, such as separate connection pools, whereas a cell isolates the entire stack.

_Usage:_

"One customer's bulk import took the API down for everyone again."

"If we move to cells, that import only affects the customers in its cell."

## Section 9 — Architecture Practice

### Software architecture

Software architecture is the structure of a software system: its major parts, how they relate, and the decisions that shape how it behaves and changes. In practice, the term covers decisions that are expensive to reverse, such as how the system is divided, where data lives and how components communicate.

There is no sharp line between architecture and design. A useful test is the cost of changing a decision later:

| Decision                             | Cost to reverse           | Usually considered |
| ------------------------------------ | ------------------------- | ------------------ |
| Name of a private function           | Minutes                   | Code detail        |
| Internal class structure of a module | Hours to days             | Design             |
| Public API contract                  | Weeks, involves consumers | Architecture       |
| Monolith or microservices            | Months                    | Architecture       |
| Primary data store                   | Months or longer          | Architecture       |

Architecture largely determines a system's [quality attributes](#quality-attribute), such as performance, availability, security and modifiability. A system can satisfy every functional requirement and still fail because its structure cannot meet them. One example is an application that works in a demo but cannot handle production traffic because every request joins across one shared database. Another is a small product change that requires edits in ten services, which points to misplaced boundaries and high [coupling](#coupling).

Most architectural work is a series of [architectural trade-offs](#architectural-trade-off), where gaining one quality costs another. Because the reasoning is easy to lose, teams record significant choices in an [architecture decision record](#architecture-decision-record).

Every codebase has an architecture, whether or not anyone designed it. Without attention, the structure tends toward a [big ball of mud](#big-ball-of-mud). It is also shaped by the organisation that builds it, as described by [Conway's law](#conways-law). An architecture is judged against the system's goals and constraints, so a design suited to a large platform can be a poor choice for a three-person product.

_Usage:_

"Should this go to an architecture review, or can we decide in the PR?"

"How hard is it to undo? Renaming a class is fine. Changing the data store needs a review."

### Architecture decision record

An architecture decision record (ADR) is a short document that captures one significant technical decision, the context that led to it and its consequences. Michael Nygard proposed the format in 2011. ADRs are usually numbered Markdown files stored in the repository, for example `docs/adr/0012-use-postgres-for-orders.md`.

ADRs address lost reasoning. A new engineer asks why orders go through a queue, nobody who made the choice is still on the team, and the group either reopens a settled debate or removes a constraint that existed for a reason. A record lets them read what was known at the time.

| Section      | Contents                                                  |
| ------------ | --------------------------------------------------------- |
| Title        | The decision, in a short phrase                           |
| Status       | Proposed, accepted, deprecated or superseded              |
| Context      | Forces and constraints at the time                        |
| Decision     | What the team will do                                     |
| Consequences | What becomes easier and harder, including costs accepted  |

```markdown
# 12. Use Postgres for orders

Status: Accepted

Context: Orders need multi-row transactions. The team already runs Postgres.

Decision: Store orders in Postgres rather than DynamoDB.

Consequences: Joins and transactions are simple. Write scaling is limited to one primary.
```

Treat accepted records as immutable. When a decision changes, write a new ADR that supersedes the old one, and change only the old record's status. The sequence then shows how the team's thinking developed.

Write an ADR for choices that are costly to reverse or that affect [quality attributes](#quality-attribute), such as data stores, integration styles and module boundaries. Do not write one for routine implementation choices, or the collection becomes noise. The Consequences section should name what was given up, because a later reader needs to know the [architectural trade-off](#architectural-trade-off) that was accepted. Keeping records in the repository lets them be reviewed in pull requests alongside the code they affect.

_Usage:_

"Why are we using a queue here instead of a direct call? Can I remove it?"

"Check ADR 31 first. It records the outage that led to it."

### Quality attribute

A quality attribute is a measurable property of a system that describes how well it performs its function, rather than what the function is. Examples include performance, availability, security, modifiability, scalability and testability. The term overlaps with non-functional requirement, and architects often prefer it because these properties drive structural decisions.

Unstated quality attributes are a frequent source of late surprises. A feature passes every test, ships, and then times out on the first busy day, because "it should be fast" was never turned into a number. A vague goal gives the team nothing to design for or verify.

To make an attribute usable, express it as a concrete scenario with a stimulus, a context and a measurable response:

| Attribute     | Example scenario                                                     |
| ------------- | -------------------------------------------------------------------- |
| Performance   | At 2,000 requests per second, 99% of checkouts finish within 400 ms  |
| Availability  | If one zone fails, service recovers within 60 seconds                |
| Modifiability | A new payment provider can be added in one module within a week      |
| Security      | After 5 failed logins in a minute, further attempts are blocked      |
| Testability   | The domain test suite runs without network access in under 2 minutes |

Quality attributes conflict. Replication improves availability but complicates consistency, encryption improves security but adds latency, and caching improves read performance but serves staler data. Because these are [architectural trade-offs](#architectural-trade-off), rank the attributes for the specific system rather than asking for all of them at maximum. An internal admin tool and a payment gateway should not have the same targets.

Once targets exist, check them continually. A [fitness function](#fitness-function), such as a latency threshold in a load test, turns a scenario into an automated check. For high-stakes systems, the [Architecture Tradeoff Analysis Method](#architecture-tradeoff-analysis-method) evaluates a design formally against prioritised scenarios.

_Usage:_

"The requirement says the dashboard must be fast. What does that mean?"

"Ask for a number. If it's two seconds at p95 for 500 users, we can design and test for that."

### Architectural trade-off

An architectural trade-off is a design decision in which improving one property of a system reduces another. Most structural choices involve one: a design that improves [quality attributes](#quality-attribute) such as availability or scalability usually costs simplicity, consistency, latency or money.

| Choice                            | Gains                                 | Costs                                     |
| --------------------------------- | ------------------------------------- | ----------------------------------------- |
| Microservices over a monolith     | Independent deployment, team autonomy | Network failures, operational load        |
| Read replicas                     | Read capacity                         | Stale reads                               |
| Caching                           | Lower latency and load                | Invalidation complexity, stale data       |
| Asynchronous messaging            | Load smoothing, looser dependencies   | Eventual consistency, harder debugging    |
| Strong consistency across regions | Correct reads everywhere              | Higher write latency, outages in partitions |
| Shared library                    | Less duplication                      | [Coupling](#coupling) between consumers |

Trade-offs that go unstated tend to surface later as surprises. A team adopts an event bus because it is considered good practice, then discovers months later that support cannot explain why an order's status differs between two screens. The cost was present from the day of the decision, but nobody named it or agreed it was acceptable.

To make a trade-off deliberately, start with the qualities the system needs most and rank them. List realistic options, including the simplest one, and state what each gives up. Prefer evidence from a prototype, load test or production data over general reputation. Then record the reasoning in an [architecture decision record](#architecture-decision-record), including the conditions under which the decision should be revisited.

Context decides the answer. Eventual consistency may be acceptable for a social feed and unacceptable for account balances. Copying a design from a large technology company imports trade-offs chosen for that company's scale and team structure, which can become [cargo cult programming](#cargo-cult-programming). For a reversible decision, choose quickly and adjust. For an expensive one, consider waiting until the [last responsible moment](#last-responsible-moment).

_Usage:_

"Let's make this asynchronous. It'll be more scalable."

"It will, but users may see stale status. Is that acceptable for refunds?"

### Fitness function

A fitness function is an automated check that measures how well a system meets a chosen architectural property. The term comes from evolutionary computing and was applied to [evolutionary architecture](#evolutionary-architecture) by Neal Ford, Rebecca Parsons and Patrick Kua in their 2017 book on the subject.

It addresses rules that exist only in documents. A wiki page says the domain layer must not import the database client, everyone agrees, and a year later a search finds forty violations added under deadline. A fitness function fails the build on the first one.

```typescript
import { test, expect } from "vitest";
import { findImports } from "./tools/imports";

test("domain code does not depend on infrastructure", async () => {
  const imports = await findImports("src/domain/**/*.ts");
  const violations = imports.filter((i) => i.target.startsWith("src/infrastructure"));
  expect(violations).toEqual([]);
});
```

| Property     | Example check                                                       | When it runs           |
| ------------ | ------------------------------------------------------------------- | ---------------------- |
| Structure    | No [circular dependencies](#circular-dependency) between modules | Every build            |
| Performance  | p95 latency stays under a threshold in a load test                  | Nightly or pre-release |
| Security     | No dependency with a known critical vulnerability                   | Every build            |
| Availability | Service survives loss of one instance in a chaos test               | Scheduled              |
| Size         | Frontend bundle stays within a budget                               | Every build            |

Useful fitness functions measure something the team has agreed matters, give a clear failure message and run at a frequency proportional to their cost. A check that fails randomly, or blocks work for a property nobody cares about, gets disabled and then protects nothing. When introducing a rule to an existing codebase, record a baseline of known violations, prevent new ones and reduce the count over time.

Fitness functions enforce decisions but do not make them. Derive each one from a prioritised [quality attribute](#quality-attribute), and retire it if the goal changes. Run continuously, they also detect [architectural drift](#architectural-drift) as it happens.

_Usage:_

"We agreed the domain wouldn't import Prisma, and I just found it in six files."

"Add an import check to CI, so the seventh fails the build."

### Evolutionary architecture

Evolutionary architecture is an approach that designs a system to support guided, incremental change over time. Neal Ford, Rebecca Parsons and Patrick Kua set it out in _Building Evolutionary Architectures_ (2017).

The approach responds to requirements, tools and scale changing in ways nobody can predict at the start. A design fixed up front tends to fit the first version of the product and resist later ones. Teams then experience a familiar cycle: the system grows harder to change until a rewrite is proposed, and the rewrite starts the same cycle.

| Element                                    | What it means                                  | Example                               |
| ------------------------------------------ | ---------------------------------------------- | ------------------------------------- |
| Incremental change                         | Small, frequent, reversible changes            | Continuous delivery, feature flags    |
| [Fitness functions](#fitness-function) | Automated checks protecting chosen qualities   | Build fails on a forbidden dependency |
| Appropriate [coupling](#coupling)      | Boundaries that let parts change independently | Modules with explicit contracts       |

The method pairs freedom to change with automated guardrails. A team can replace a component or reshape a module because its fitness functions show whether performance, security and structure are still acceptable. Without these checks, incremental change is unguided and tends to produce [architectural drift](#architectural-drift).

Evolutionary architecture is not the absence of design. Teams still make and record structural decisions, but they defer irreversible ones to the [last responsible moment](#last-responsible-moment) and prefer choices that are cheap to undo. A large migration proceeds in stages, for example using a strangler fig to replace one route at a time while the old system serves the rest.

The approach has costs. It depends on a reliable delivery pipeline, good test coverage and time to maintain the checks, and a team that deploys quarterly cannot evolve in small steps. Some decisions, such as a public API or a data model shared with partners, remain expensive however the system is built, so they warrant more care up front. For a short-lived or stable system, the investment may not pay off.

_Usage:_

"We keep saying the next rewrite will finally get the structure right."

"Let's stop betting on a rewrite. Add checks for the boundaries we care about and move one module at a time."

### C4 model

The C4 model is a way of diagramming [software architecture](#software-architecture) at four levels of zoom: context, containers, components and code. Simon Brown created it. Each level answers a different question for a different audience, in the way a map can zoom from a country to a street.

It addresses diagrams that cannot be read without their author. A whiteboard photo with unlabelled boxes and arrows may mix a database, a team, a Kubernetes cluster and a class at the same level, and two engineers will interpret it differently.

| Level             | Shows                                                    | Audience                     |
| ----------------- | -------------------------------------------------------- | ---------------------------- |
| 1. System context | The system, its users and external systems               | Everyone, including non-technical people |
| 2. Container      | Separately running units and how they communicate        | Engineers, operations        |
| 3. Component      | Major building blocks inside one container               | Engineers working on it      |
| 4. Code           | Classes or functions in one component                    | Rarely drawn by hand         |

A container in C4 is not a Docker container. It means something that must be running for the system to work, such as a web app, an API, a database or a message broker.

The model does not prescribe a notation. It asks that each element has a name, type, technology and short description, and that each arrow has a label saying what the relationship does. "Sends order events to" is more informative than an unlabelled line.

Levels 1 and 2 are enough for many teams. Level 3 helps with complex containers, and level 4 is usually generated from code or omitted because it goes stale quickly. Keeping diagrams as code in the repository, with a tool such as Structurizr or Mermaid, means they are reviewed alongside changes and reduces [architectural drift](#architectural-drift) between the diagram and the system. C4 describes structure only, so pair it with an [architecture decision record](#architecture-decision-record) to explain why that structure exists.

_Usage:_

"Is this box on the diagram a service, a database or a team?"

"Redraw it as a C4 container diagram and label every box and arrow."

### Architecture Tradeoff Analysis Method

The Architecture Tradeoff Analysis Method (ATAM) is a structured review for evaluating a software design against its [quality attribute](#quality-attribute) goals. It was developed at the Software Engineering Institute at Carnegie Mellon University. An evaluation team works with architects and stakeholders to find where a design puts those goals at risk, before the cost of changing it grows.

ATAM suits major commitments where a late structural flaw would be expensive, such as a multi-year platform. The failure it guards against is discovering at acceptance testing that an approved design cannot meet its throughput or failover requirements, after the budget has been spent building it.

| Phase                 | Who                                | What happens                                                        |
| --------------------- | ---------------------------------- | ------------------------------------------------------------------- |
| 0. Preparation        | Evaluation and project leaders     | Agree scope, logistics and participants                             |
| 1. Evaluation         | Evaluators, architects, project leads | Present drivers and design, build a utility tree, analyse approaches |
| 2. Wider evaluation   | The above plus stakeholders        | Brainstorm and rank scenarios, analyse again, present results       |
| 3. Follow-up          | Evaluation team, sponsor           | Deliver the written report                                          |

The analysis produces specific findings rather than a pass or fail:

| Output            | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| Sensitivity point | A decision that strongly affects one quality               |
| Trade-off point   | A decision that affects several qualities in opposing ways |
| Risk              | A decision that may cause a problem                        |
| Non-risk          | A decision judged safe, with the reasons                   |
| Risk theme        | A pattern across risks, tied to business drivers           |

ATAM is costly, because it involves many people over several days plus preparation. Most product teams do not need the full method. A lighter version keeps the useful parts: write the top five scenarios, walk the design through each, and capture each [architectural trade-off](#architectural-trade-off) in an [architecture decision record](#architecture-decision-record). ATAM evaluates a design but does not produce one, and it does not replace measuring the built system.

_Usage:_

"We're committing three years of budget to this platform design. How do we test it on paper?"

"Run an ATAM with the stakeholders, or at least walk the top failover scenarios through the design."

### Conway's law

Conway's law states that an organisation designing a system will produce a design whose structure mirrors the organisation's communication structure. Melvin Conway published the observation in 1968 in the article "How Do Committees Invent?".

The mechanism is communication cost. Engineers on one team can adjust a shared interface in a conversation, so code within a team tends to be tightly integrated. Across teams, changes require meetings and agreements, so teams settle on narrow interfaces at their boundary. Over time, module boundaries settle where the team boundaries are.

The effect is visible when a simple feature needs changes from three teams and waits in three backlogs, because the system was divided along the org chart rather than along the problem. A website whose navigation follows company departments instead of user tasks is another example.

| Organisation                                 | Likely architecture                      |
| -------------------------------------------- | ---------------------------------------- |
| Separate frontend, backend and database teams | Layers with handoffs at each boundary    |
| One team per business capability             | Services aligned with capabilities       |
| A single team across the product             | A monolith with fluid internal boundaries |
| Outsourced vendor for one subsystem          | A formal, rigid interface at the contract line |

Conway's law describes a tendency rather than a strict rule. Deliberate interfaces and technical leadership can work against it, but a design that conflicts with how teams communicate needs continuous effort to maintain. A [distributed monolith](#distributed-monolith) often appears when a system is split into services while the same people and approvals still coordinate every release.

Treat the org chart as an architectural input. Before approving a target design, check whether teams can own its parts with little coordination. If they cannot, change the design or the teams. Changing teams deliberately to obtain a design is the [inverse Conway maneuver](#inverse-conway-maneuver), and [Team Topologies](#team-topologies) offers a vocabulary for that work.

_Usage:_

"Why does adding a shipping option need the web, orders and logistics teams?"

"The system is split the way we're organised. That's Conway's law."

### Inverse Conway maneuver

The inverse Conway maneuver is the practice of restructuring teams so that their communication paths produce a desired software design. It applies [Conway's law](#conways-law) in reverse: instead of letting the organisation determine the design, leaders choose the design and shape the organisation to match.

It addresses architecture plans that fail against the existing org chart. A company draws independent services on a whiteboard, but one shared database team must approve every schema change and one frontend team integrates every feature. The services deploy separately in name only, and the result is a [distributed monolith](#distributed-monolith).

| Step                   | Who                           | What happens                                               |
| ---------------------- | ----------------------------- | ---------------------------------------------------------- |
| 1. Define the target   | Architects, engineering leads | Identify boundaries that should change independently       |
| 2. Map the gap         | Engineering leads             | Compare current team communication with those boundaries   |
| 3. Redraw teams        | Leadership                    | Give each team end-to-end ownership of one boundary        |
| 4. Move ownership      | Teams                         | Transfer code, data and on-call responsibility             |
| 5. Reduce coordination | Teams                         | Replace shared approvals with contracts and self-service tools |
| 6. Review              | Engineering leads             | Check whether changes now stay within one team             |

[Team Topologies](#team-topologies) provides team types and interaction modes for step 3.

The main risk is choosing the wrong boundary. Once a team owns a boundary, people, roadmaps and code all reinforce it, so a mistaken split becomes expensive to change. Validate a boundary first by examining which code changes together and by trying it in one area of the business. A [context map](#context-map) can help identify candidates.

A reorganisation also has costs: lost working relationships, interrupted delivery and displaced knowledge. Do not use the maneuver on a small codebase, or where the current structure causes no coordination problems. Moving people without the matching technical work achieves little, because the old code keeps forcing teams to coordinate, so move ownership and code together.

_Usage:_

"We split into services, but every release still needs the DBA team's approval."

"The team structure didn't change. Give each domain team ownership of its schema and deployments."

### Team Topologies

Team Topologies is a model for organising software teams around the flow of delivery, introduced by Matthew Skelton and Manuel Pais in their 2019 book of the same name. It defines four team types and three interaction modes, and treats team cognitive load as the main limit on what any team should own.

| Team type             | Purpose                                                            |
| --------------------- | ------------------------------------------------------------------ |
| Stream-aligned        | Delivers a flow of change for one product, service or user journey |
| Platform              | Provides internal services that reduce work for other teams        |
| Enabling              | Helps other teams acquire new skills, then moves on                |
| Complicated-subsystem | Owns a part that needs deep specialist knowledge                   |

| Interaction mode | Meaning                                 | Suited to                       |
| ---------------- | --------------------------------------- | ------------------------------- |
| Collaboration    | Two teams work closely for a period     | Discovering a new boundary      |
| X-as-a-Service   | One team consumes what another provides | Stable, well-defined boundaries |
| Facilitating     | One team coaches another                | Closing a skill gap             |

Cognitive load is the amount of information a team must hold to do its work. When one team owns a dozen services, their pipelines, on-call and a legacy system, each change means rediscovering how something works, and delivery slows. The remedy is to reduce what the team owns, by narrowing its scope or moving undifferentiated work to a platform.

Stream-aligned teams are the default, and the other three types exist to reduce their burden. A common failure is a platform that teams are forced to use and that needs a ticket for routine work. Run a platform as a product with internal customers.

The model builds on [Conway's law](#conways-law), because team boundaries shape system boundaries, and it gives vocabulary for an [inverse Conway maneuver](#inverse-conway-maneuver). Interactions are expected to change, for example from collaboration while a boundary is explored to X-as-a-Service once it settles. Renaming existing teams without changing ownership or interactions has no effect.

_Usage:_

"Our team owns fourteen services and nobody understands all of them."

"That's too much cognitive load. Move the shared infrastructure to a platform team and narrow our scope."

### Walking skeleton

A walking skeleton is a minimal implementation of a system that performs one small function end to end through all its main architectural components. Alistair Cockburn described the term. For an online shop, it might be a page that submits a hard-coded order through the API and a queue to a database, deployed by the real pipeline to a real environment.

It addresses integration problems that surface late. Teams build the frontend, API and data layer separately for months, each passing its own tests, and then discover during integration that authentication, message formats or deployment do not fit together. A walking skeleton forces those connections to work in the first days, when changing them is inexpensive.

To build one, pick the thinnest feature that touches each main component. Stub the business logic but keep the connections real: network calls, database access, configuration, deployment and monitoring. Run it in a production-like environment, then add features by thickening it, keeping the system runnable throughout.

| Technique              | Purpose                                    | Kept afterward?                 |
| ---------------------- | ------------------------------------------ | ------------------------------- |
| Walking skeleton       | Prove the architecture connects end to end | Yes, it grows into the product  |
| Prototype              | Answer a design or usability question      | Usually discarded               |
| Spike                  | Investigate one technical unknown          | Code discarded, learning kept   |
| Minimum viable product | Test whether users want the product        | Yes, and it provides user value |

The skeleton is not expected to be useful to users. It provides evidence that the chosen structure works, a deployment path from the start, and a shared running system for parallel teams to integrate against. It is a practical first step in an [evolutionary architecture](#evolutionary-architecture).

It helps less for a small change inside an established system, where the structure and pipeline already exist. Keep it thin. Adding real features before all components connect, or building abstractions for future needs, turns it into ordinary development and invites [speculative generality](#speculative-generality).

_Usage:_

"Every team is green on its own, but nothing has run together yet."

"Stop adding features. Get one hard-coded order through the whole stack and deployed this week."

### Architectural drift

Architectural drift is the gradual divergence between a system's intended architecture and the structure actually present in its code. It usually happens through many small, locally reasonable changes rather than one bad decision.

The usual symptom is a diagram that no longer matches the system. The document shows controllers calling services and services calling repositories, but a new engineer finds controllers running SQL directly and two supposedly independent modules importing each other. Estimates grow, because the real dependencies stay invisible until a change breaks something.

Drift comes from deadline shortcuts, staff turnover and rules that exist only in people's heads. Coding agents can accelerate it, because they tend to copy whichever pattern they find nearby, including a violation.

| Term    | Meaning                                                     | Example                                                  |
| ------- | ----------------------------------------------------------- | -------------------------------------------------------- |
| Drift   | Code departs from the design's intent without breaking a stated rule | A utility module slowly accumulates business logic |
| Erosion | Code violates an explicit architectural constraint          | The UI imports the database client despite a layering rule |

Some authors use the two terms interchangeably.

Detect drift by comparing the design with the code. Dependency analysis tools show the actual import graph, and change history shows modules that always change together. A [fitness function](#fitness-function) that checks allowed dependencies can then stop new violations in CI.

Each gap needs a decision, because the code is not always the wrong side. If the code reflects a better understanding of the domain, update the diagram and record the change in an [architecture decision record](#architecture-decision-record). If it is an accidental violation, fix it, or log it as [technical debt](#technical-debt) with an owner. Left unmanaged for years, drift tends toward a [big ball of mud](#big-ball-of-mud).

_Usage:_

"The diagram says billing only talks to orders through its API."

"It did two years ago. Billing now reads the orders table directly in four places."

### Technical debt

Technical debt is the future cost created by leaving code or design in a state that makes later changes slower or riskier. Ward Cunningham introduced the metaphor in 1992: shipping before the design fully reflects your understanding is like borrowing money, and the extra effort on each later change is the interest.

The symptom is delivery that slows while the team stays the same size. Features that took days now take weeks, engineers avoid a particular module, and fixing one bug produces another. The principal is the work needed to fix the design. The interest is paid whenever someone has to work around it.

Debt has different causes. Martin Fowler's technical debt quadrant separates four kinds:

|             | Reckless                        | Prudent                                       |
| ----------- | ------------------------------- | --------------------------------------------- |
| Deliberate  | "We don't have time for design" | "We must ship now and deal with consequences" |
| Inadvertent | "What's Layering?"              | "Now we know how we should have done it"      |

Deliberate, prudent debt can be a sound [architectural trade-off](#architectural-trade-off), for example hard-coding a tax rate to test a market before building a tax engine. It stays sound only if someone records it and returns to it. Cunningham's original meaning was closer to the bottom right: code written with the understanding available at the time, then refactored as understanding improves. Code that is simply careless is a different problem, and calling it debt can hide that.

Manage debt according to where it charges interest. Code that is ugly but stable costs little. Code that changes weekly and is hard to change costs a lot, so prioritise by combining change frequency with difficulty. Pay down debt as part of feature work in the affected area, and track larger items with an owner and a stated cost. A full rewrite carries its own risks, so prefer incremental replacement.

_Usage:_

"Why does every change to invoicing take a week?"

"We hard-coded the tax logic for launch and never went back. We're paying interest on it now."

### Reference architecture

A reference architecture is a reusable template describing the components, patterns, technology choices and decisions for a class of systems. An organisation might publish one for customer-facing web services, and cloud vendors publish them for workloads such as data lakes and web applications.

It addresses teams solving the same problems differently. Without a shared starting point, each new service invents its own logging, authentication and deployment, so on-call engineers must relearn every system and security reviews start from zero. A reference architecture gives teams a default that has already been reviewed.

| Artefact               | Scope                        | Example                             |
| ---------------------- | ---------------------------- | ----------------------------------- |
| Design pattern         | One recurring design problem | [Strategy pattern](#strategy-pattern) |
| Reference architecture | A class of systems           | Standard event-processing service   |
| Solution architecture  | One specific system          | The design of our payments service  |
| Service template       | Executable starting point    | A scaffold implementing the reference |

A useful reference architecture states what it is for, which [quality attributes](#quality-attribute) it targets, when it does not apply and why each major choice was made. Pair the document with a working example or scaffold, because teams follow code more reliably than diagrams.

The common failure is applying it regardless of fit. A small internal tool inherits a queue, three clusters and a service mesh because the template requires them, and then costs more to run than it delivers. This is a form of [golden hammer](#golden-hammer). Allow exceptions, and ask teams to explain them in an [architecture decision record](#architecture-decision-record). Frequent exceptions indicate that the reference needs revising.

Reference architectures also age. One written for a past technology stack keeps steering new work toward it unless it has an owner and a review schedule. Vendor reference architectures are designed around that vendor's products, so treat them as input rather than instruction.

_Usage:_

"Do we need the full event pipeline for this little admin tool?"

"No. The reference covers high-volume services. Record the exception and build a simple CRUD app."

### Last responsible moment

The last responsible moment is the point at which delaying a decision further would eliminate an important option or make the outcome significantly more expensive. Mary and Tom Poppendieck brought the term to software in _Lean Software Development_ (2003). The aim is to make consequential decisions with as much information as possible, while still making them in time.

It addresses decisions made early on guesses. A team picks a database, a message broker and a service split in week one, before it knows its access patterns, then spends a year working around choices made when it had the least information.

The opposite failure is waiting too long. If a team postpones choosing an identity provider until just before launch, the delay has effectively made the decision, and the remaining options are all rushed. Delay is useful only when the team uses the time to learn.

| Decision type           | Example                                       | Approach                                             |
| ----------------------- | --------------------------------------------- | ---------------------------------------------------- |
| Easily reversed         | Logging library                               | Decide now and move on                               |
| Costly but isolated     | Search engine behind an interface             | Defer, and keep it behind a clear boundary           |
| Costly and far-reaching | Tenancy model, public API, primary data store | Investigate early, decide when evidence is sufficient |
| Blocks other teams      | Shared event schema                           | Decide as soon as the dependency arises              |

To keep an option open, put the volatile choice behind an [abstraction](#abstraction), build a [walking skeleton](#walking-skeleton) to learn which constraints are real, and identify the date by which each decision must be made. Deferral has its own cost: abstractions added to preserve options can become [speculative generality](#speculative-generality), so use them only where a change is plausible.

The idea is related to [YAGNI](#yagni), which concerns not building features until they are needed. The last responsible moment concerns when to commit to a decision. When that point arrives, decide and write the reasoning in an [architecture decision record](#architecture-decision-record).

_Usage:_

"Should we choose the tenancy model now, or wait for the enterprise requirements?"

"We can wait until the first schema migration next month. After that, changing it gets expensive."

## Section 10 — Anti-Patterns

### Anti-pattern

An anti-pattern is a common response to a recurring problem that looks reasonable but produces worse results than a known alternative. The definition has two parts: the approach is widespread enough to deserve a name, and a better option exists. A one-off mistake is a bug, and a poor option with no better alternative is a constraint. The 1998 book _AntiPatterns_ by Brown, Malveau, McCormick and Mowbray popularised the term by cataloguing these approaches in a format similar to design patterns.

Anti-patterns persist because their early costs are low and their later costs often fall on someone else. Adding one more method to a [god object](#god-object) is the quickest way to finish today's ticket. The team usually notices the result months later, when small changes take days and nobody can predict what a release will break.

The term is often confused with nearby vocabulary:

| Term                                    | What it describes                           | Typical response                    |
| --------------------------------------- | ------------------------------------------- | ----------------------------------- |
| Bug                                     | Behaviour that is wrong                     | Fix it                              |
| Code smell                              | A surface sign that may indicate a problem  | Investigate                         |
| Anti-pattern                            | A recurring approach that causes harm       | Replace it with the known alternative |
| [Technical debt](#technical-debt) | A cost accepted now and repaid later        | Schedule repayment or accept it     |

Some entries in this section, such as [shotgun surgery](#shotgun-surgery) and [feature envy](#feature-envy), began as code smells, a term Kent Beck coined for Martin Fowler's _Refactoring_ (1999). A smell is a prompt to look closer and does not prove that the design is wrong.

A shared name makes design review faster, because "this is turning into a [big ball of mud](#big-ball-of-mud)" conveys a known failure and its direction. The label is not an argument by itself. A [singleton](#singleton) is called an anti-pattern by some engineers and is a reasonable choice for a process-wide logger. Before applying the label, state the specific cost the code imposes and the alternative you would use. If you cannot name both, treat the concern as a preference.

_Usage:_

"This handler queries the database directly. Isn't that an anti-pattern?"

"It's a forty-line internal script with one query. What would the alternative save us?"

### Big ball of mud

A big ball of mud is a system with no recognisable structure, in which any part can depend on any other. Brian Foote and Joseph Yoder named it in their 1997 paper "Big Ball of Mud" and treated it as a common outcome in working software, not a rare failure. The usual symptom is a change with a distant effect: a fix to invoice rounding breaks the password reset email, and nobody can explain why until they trace a chain of shared helpers.

The structure erodes through many decisions that were reasonable at the time. Deadlines, staff turnover and changing requirements each encourage a shortcut, and each shortcut adds a dependency. With no enforced boundaries, [coupling](#coupling) rises and [circular dependencies](#circular-dependency) appear. This is [architectural drift](#architectural-drift) left unchecked. New engineers need months before they can change anything alone, and tests require most of the application to start.

A big ball of mud is different from a monolith. A monolith with clear internal modules is well structured inside one deployable. A set of microservices can have no structure at all, which produces a [distributed monolith](#distributed-monolith).

A full rewrite is rarely the right response, because many business rules exist only in the code and are easy to lose. Incremental work is safer:

| Step | Action                                                                     |
| ---- | -------------------------------------------------------------------------- |
| 1    | Map the actual dependencies with a tool                                    |
| 2    | Choose one area that changes often                                         |
| 3    | Add characterisation tests that record its current behaviour               |
| 4    | Introduce a [seam](#seam) and move callers behind an interface         |
| 5    | Enforce the new boundary in CI with a [fitness function](#fitness-function) |

Repeat this for the areas that change most. Untidy code that is stable and rarely touched can stay as it is. A throwaway prototype can also be built without structure at little cost, provided it is actually thrown away.

_Usage:_

"Why did changing invoice rounding break the password reset email?"

"Both import the same utils module, and that module imports half the app. Let's map the dependencies before we change anything else."

### God object

A god object is a class that holds too much data and too many responsibilities, so most of the system depends on it. It often has a broad name such as `UserManager`, `AppService` or `OrderManager`. The symptoms are practical: every pull request conflicts in the same file, a unit test needs a dozen mocks before it can run, and nobody can state the purpose of the class in one sentence.

```typescript
class OrderManager {
  createOrder(input: OrderInput) {}
  applyDiscount(orderId: string, code: string) {}
  chargeCard(orderId: string) {}
  sendConfirmationEmail(orderId: string) {}
  generateInvoicePdf(orderId: string) {}
  syncToWarehouse(orderId: string) {}
  exportMonthlyReport(month: string) {}
}
```

This class breaks the [single responsibility principle](#single-responsibility-principle), because payment, tax, email and reporting changes all land in it. Its [cohesion](#cohesion) is low, since most methods share little state. Its [coupling](#coupling) is high, since many callers depend on it and it depends on many services. A change for one feature can therefore break another.

God objects grow because they are convenient. The class already has access to everything, so adding one more method is quicker than designing a new module. Each addition makes the next one more likely.

To break one up, group its methods by the data they use and the reason they change. Extract one group at a time into a class such as `Invoicing` or `Payments`. During the migration, the original class can act as a [facade](#facade-pattern) that delegates to the new classes, so callers can move gradually. Remove the delegating methods once nothing calls them.

Size alone does not make a class a god object. A [deep module](#deep-module) can hide a large implementation behind a small interface, and a long parser may do only one thing. A facade also has a broad reach, but it coordinates other objects and holds little logic of its own. The test is whether the responsibilities are related and change for the same reasons.

_Usage:_

"Three of us have merge conflicts in `OrderManager` again."

"It handles payments, invoices and emails. Let's extract invoicing first and have the old method delegate to it."

### Anemic domain model

An anemic [domain model](#domain-model) has objects that hold data while the business rules live in separate service classes. Martin Fowler described it as an anti-pattern in a 2003 article, because it carries the cost of a domain model, such as object mapping, without the benefit of keeping behaviour next to the data it governs.

```typescript
// Anemic: any caller can set an invalid status.
class AnemicOrder {
  status: "open" | "paid" | "shipped" = "open";
}

class OrderService {
  ship(order: AnemicOrder) {
    if (order.status !== "paid") throw new Error("Order is not paid");
    order.status = "shipped";
  }
}

// Rich: the rule lives with the state it protects.
class Order {
  #status: "open" | "paid" | "shipped" = "open";

  ship() {
    if (this.#status !== "paid") throw new Error("Order is not paid");
    this.#status = "shipped";
  }
}
```

The usual symptom is a rule enforced in one path and skipped in another. The checkout service checks that an order is paid before shipping, but a batch job or admin tool sets `status = "shipped"` directly, and unpaid orders go out. The [invariant](#invariant) is unprotected because the object has no [encapsulation](#encapsulation), so each new caller must know and repeat the rule.

To fix it, replace public setters with named methods such as `ship()` and move each rule onto the object whose data it checks. Keep a [domain service](#domain-service) for rules that span several objects and have no natural owner.

The pattern is not always a mistake. For an application that is mostly create, read, update and delete, plain data with a [transaction script](#transaction-script) is simpler and adequate. Functional codebases also separate data from functions by design, and can protect rules with immutable types and validated constructors. The anti-pattern applies when the domain has complex rules, the team maintains a model, and the rules are still scattered outside it.

An anemic object also differs from a [data transfer object](#data-transfer-object). A data transfer object is meant to carry no behaviour, because its job is to move data across a boundary.

_Usage:_

"Support found shipped orders that were never paid."

"The admin tool sets `status` directly. Move the check into `order.ship()` and make the field private."

### Distributed monolith

A distributed monolith is a system split into separately deployed services that are so tightly coupled they must change, release or fail together. It carries the operational cost of microservices without their independence. The typical symptom is a release checklist: shipping one feature requires deploying six services in a fixed order, and one service being down stops the checkout flow.

The usual causes are specific and detectable:

| Cause                            | What happens                                  | Alternative                                 |
| -------------------------------- | --------------------------------------------- | ------------------------------------------- |
| Shared database                  | A schema change breaks other services         | Each service owns its data                  |
| Long synchronous call chains     | One slow service stalls every caller          | Use asynchronous messaging or merge them    |
| Shared domain library            | A version bump forces every service to deploy | Share only small, stable contracts          |
| Services split by technical layer | One feature touches every service            | Split by business capability                |
| Unversioned API changes          | Producer and consumers must deploy together   | Make backward-compatible changes            |

The problem usually starts with where the boundaries were drawn. A monolith split by database table or technical layer, instead of by [subdomain](#subdomain), keeps its [coupling](#coupling) and moves it onto the network. [Conway's law](#conways-law) also applies: when service boundaries do not match team boundaries, routine changes need coordination across teams.

This outcome is usually worse than the monolith it replaced. Function calls become network calls, so the system gains latency, partial failure and harder debugging, while teams still cannot release independently. A [big ball of mud](#big-ball-of-mud) spread over a network is harder to change than one in a single process.

To diagnose it, use commit and deployment history to find services that always change together. Those services are candidates for merging. For the rest, remove shared tables and shorten synchronous call chains. A useful test is whether a team can deploy its service on an ordinary day without coordinating with another team. For a small organisation, a modular monolith is often a better destination than repairing many services.

_Usage:_

"Adding a field to the customer record needs deploys of six services, in order."

"Then they're one system. Let's start by merging the three that always change together."

### Spaghetti code

Spaghetti code is code whose control flow is so tangled that a reader cannot follow what happens next without jumping between many places. The term dates from unstructured programming, when `goto` could transfer control anywhere. Edsger Dijkstra argued against that style in his 1968 letter "Go To Statement Considered Harmful". Modern code produces the same effect through deep nesting, boolean flags, callbacks, shared mutable state and event handlers that trigger each other.

The symptom appears during debugging. To learn why an order was charged twice, an engineer steps through a function, finds a flag changed halfway down, and then finds that the function calls itself with different arguments.

```typescript
function process(order: Order, retry: boolean, skipTax: boolean) {
  let ok = false;
  if (order.items.length) {
    if (!skipTax) {
      order.tax = calcTax(order);
      if (order.tax < 0) retry = true;
    }
    if (!retry || order.attempts < 3) {
      ok = charge(order);
      if (!ok && retry) return process(order, false, true);
    }
  }
  if (ok) notify(order);
  return ok;
}
```

Because the behaviour is unclear, start by writing tests that record what the code does today. Then simplify in small steps. Use guard clauses to reduce nesting, extract named functions for each stage, and replace boolean parameters with separate functions. When behaviour depends on a status that changes over time, an explicit state machine or the [state pattern](#state-pattern) makes the allowed transitions visible.

Spaghetti code differs from a [big ball of mud](#big-ball-of-mud) in scale. Spaghetti describes control flow inside a function or module, while a big ball of mud describes the structure of a system. A system can have clean module boundaries with one tangled module inside, or tidy functions connected by chaotic dependencies.

Length alone does not make code spaghetti. A hundred-line function that reads from top to bottom can be easier to follow than ten small functions that call each other in a loop. Cyclomatic complexity can flag candidates, but the practical test is whether someone can predict the path through the code without running it.

_Usage:_

"Why was this order charged twice?"

"`retry` changes halfway through and the function calls itself. Let's split it into explicit steps before we fix the bug."

### Lava flow

Lava flow is dead or obsolete code that stays in a system because nobody knows whether removing it is safe. The name, used in the 1998 book _AntiPatterns_, compares this code to lava that has cooled and hardened, so later work builds on top of it. It shows up as files named `handler_old` or `pricing_v2`, a config flag nobody can explain, and a comment reading "do not delete, not sure why".

This code usually comes from experiments and migrations that were never finished. A strangler fig migration that stops halfway, for example, leaves two paths in production. The original authors move on, and each later engineer leaves the code alone because deleting it might break something.

Keeping it has a continuing cost and forms part of a system's [technical debt](#technical-debt). Engineers read and maintain code that does nothing, searches return false leads, and libraries used only by dead code still need security patches. Dormant paths can also be triggered by accident.

Removal is safe when it follows a sequence of checks:

| Step    | What to do                                                            |
| ------- | --------------------------------------------------------------------- |
| Search  | Find references, including reflection, dynamic imports and config     |
| Observe | Add a log or metric to the path and watch a full business cycle       |
| Disable | Put the path behind a flag and switch it off in production            |
| Delete  | Remove the code, knowing version control keeps the history            |
| Prevent | Give each experiment and migration an owner and a removal date        |

The observation period matters because some code runs rarely. A path that looks unused for three weeks may belong to a month-end or year-end job.

Old code is not automatically lava flow. Legacy code that is in use and understood is simply legacy code. Lava flow also differs from [speculative generality](#speculative-generality), which is code built for a future need that never arrived. Lava flow is usually left behind by past work that was abandoned or replaced.

_Usage:_

"Can we delete `pricing_v2`? I can't find anything that calls it."

"The quarter-end job loads modules by name. Add a log and wait until that job has run."

### Golden hammer

A golden hammer is one familiar tool, technology or pattern applied to every problem, including problems it fits poorly. The name comes from the saying that if all you have is a hammer, everything looks like a nail. The symptoms include a search feature built on `LIKE '%term%'` that slows down with each new customer, a message queue used for simple function calls, and design meetings where the tool is chosen before anyone states the requirement.

The habit has understandable causes. The team knows the tool, has already invested in it and has seen it succeed. Hiring, vendor contracts and existing infrastructure all reinforce the choice, so the previous success feels like evidence for the next problem.

Standardising on a few tools is often the right decision, and it should not be confused with this anti-pattern. Every additional technology adds operational work, training and failure modes. Using an existing relational database for a modest job queue can be a sound choice. The difference lies in how the decision was made:

| Signal         | Reasonable standardisation                                | Golden hammer                     |
| -------------- | --------------------------------------------------------- | --------------------------------- |
| Why chosen     | Compared against the requirements                         | Chosen before requirements existed |
| Fit            | Meets the needed [quality attributes](#quality-attribute) | Needs growing workarounds         |
| Costs          | Known and accepted                                        | Not discussed                     |
| Exceptions     | Allowed with a written reason                             | Refused by default                |

To avoid it, write down the requirements before choosing a tool, including expected load and failure behaviour. Compare at least two options, one of which can be the current tool, and record the outcome in an [architecture decision record](#architecture-decision-record). Revisit the choice when workarounds start to accumulate.

The same habit applies to design patterns. An engineer who has just learned the [strategy pattern](#strategy-pattern) may start using it for a single `if` statement. A golden hammer differs from [cargo cult programming](#cargo-cult-programming), where a practice is copied without understanding it. The golden hammer user may understand the tool well and still apply it too widely.

_Usage:_

"Search takes nine seconds now. Should we add another index to the orders table?"

"That's the fourth workaround. Let's compare it against a dedicated search engine before adding a fifth."

### Shotgun surgery

Shotgun surgery is a code smell in which one logical change forces many small edits across many classes or files. Martin Fowler and Kent Beck listed it in _Refactoring_ (1999). A typical case is adding a payment method and having to touch the checkout form, API validator, fee calculation, receipt template, report export and admin filter. The bug report after release concerns the one place that was missed.

```typescript
// Before: each file holds its own knowledge of payment methods.
const checkoutOptions = ["card", "paypal"]; // checkout.ts
const isValid = (m: string) => m === "card" || m === "paypal"; // api.ts
const feeRate = (m: string) => (m === "card" ? 0.029 : 0.034); // pricing.ts

// After: one definition that every file reads.
const paymentMethods = {
  card: { label: "Card", feeRate: 0.029 },
  paypal: { label: "PayPal", feeRate: 0.034 },
} as const;

type PaymentMethod = keyof typeof paymentMethods;
```

The cause is one decision spread across many modules, which is a form of low [cohesion](#cohesion). Often the same knowledge has been duplicated, so [DRY](#dry) applies. Layering can cause it too: in a strict layered architecture, adding one field may mean editing a controller, data object, service, repository and mapper. [Package by feature](#package-by-feature) and [vertical slice architecture](#vertical-slice-architecture) reduce this by keeping code that changes together in one place.

To fix it, move the scattered pieces of the decision into one module. Where behaviour varies by type, use a lookup table or the [strategy pattern](#strategy-pattern). When full consolidation is not sensible, make the compiler find the sites: a value typed `Record<PaymentMethod, Rate>` fails to compile until each method has an entry, which turns a forgotten edit into a build error.

_Refactoring_ pairs this smell with divergent change, its mirror image. Divergent change is one class edited for many unrelated reasons, as seen in a [god object](#god-object). Shotgun surgery is one reason requiring edits to many classes.

Some wide changes are legitimate. Renaming a shared API field touches every caller once and does not indicate a design problem. The smell is the same kind of change fanning out repeatedly.

_Usage:_

"We added the new payment method and refunds broke."

"Refunds had their own copy of the list. That's the sixth file for one change. Let's define the methods in one place."

### Feature envy

Feature envy is a code smell in which a method uses another object's data more than its own, which suggests the method belongs on that other object. Martin Fowler and Kent Beck described it in _Refactoring_ (1999). It is recognisable when every line of a method starts with `customer.`, and when renaming a field on `Customer` forces edits in `InvoiceService`.

```typescript
// Envious: the rule reads only Customer data.
class InvoiceService {
  discountRate(customer: Customer): number {
    if (customer.isSuspended) return 0;
    if (customer.loyaltyYears >= 5) return 0.1;
    return customer.orderCount > 20 ? 0.05 : 0;
  }
}

// Moved: the rule sits with the data it reads.
class Customer {
  discountRate(): number {
    if (this.isSuspended) return 0;
    if (this.loyaltyYears >= 5) return 0.1;
    return this.orderCount > 20 ? 0.05 : 0;
  }
}
```

The envious version forces `Customer` to expose its fields, which weakens [encapsulation](#encapsulation) and adds [coupling](#coupling) between the two classes. A change to loyalty rules also lands in a class about invoices. [Tell don't ask](#tell-dont-ask) gives the matching guidance: ask an object to do the work instead of pulling its data out. Long chains such as `order.customer.address.city` often accompany this smell and break the [Law of Demeter](#law-of-demeter). When envy is repeated across a codebase, the result is an [anemic domain model](#anemic-domain-model).

To fix it, move the method to the class whose data it uses. If only part of the method is envious, extract that part and move it. If a method uses data from two objects, place it with the data that changes alongside the rule.

Some designs separate behaviour from data on purpose. A [visitor](#visitor-pattern) reads other objects' data so that operations can vary independently of them. A report formatter also reads many `Customer` fields, but moving it onto `Customer` would pull presentation into the domain and work against [separation of concerns](#separation-of-concerns). Ask what causes the code to change. If it changes with customer rules, move it. If it changes with the report layout, leave it.

_Usage:_

"`discountRate` is in `InvoiceService`, but it only reads `Customer` fields."

"And it changes whenever the loyalty rules change. Move it onto `Customer`."

### Primitive obsession

Primitive obsession is the use of strings, numbers and booleans to represent domain concepts that should have their own types. Martin Fowler and Kent Beck listed it as a code smell in _Refactoring_ (1999). Common examples are money stored as a `number`, email addresses as a `string` and identifiers as plain strings. The symptoms are concrete: a caller swaps `userId` and `orderId` and the compiler accepts it, an amount in cents is added to an amount in euros, and the same email regex appears in four files with small differences.

```typescript
// Compiles, even with the arguments in the wrong order.
function transfer(from: string, to: string, amount: number) {}
transfer(customerId, accountId, priceInCents);

// A branded type stops one kind of ID being passed as another.
type AccountId = string & { readonly __brand: "AccountId" };

// A value object validates once and carries its operations.
class Money {
  private constructor(readonly cents: number, readonly currency: "EUR" | "USD") {}

  static of(cents: number, currency: "EUR" | "USD") {
    if (!Number.isInteger(cents)) throw new Error("Cents must be an integer");
    return new Money(cents, currency);
  }

  add(other: Money) {
    if (other.currency !== this.currency) throw new Error("Currency mismatch");
    return new Money(this.cents + other.cents, this.currency);
  }
}
```

The usual fix is a [value object](#value-object). It wraps the primitive, validates at construction so that its [invariant](#invariant) holds wherever the value travels, and provides the operations that make sense for it. `Money` can refuse to add two currencies, which a `number` cannot do. For identifiers that need no behaviour, a branded type in TypeScript gives compile-time safety at no runtime cost.

Wrapping has a cost. Values must be converted at boundaries such as database rows, JSON and form input. Parse them once at the boundary and pass the typed value from then on. A [data transfer object](#data-transfer-object) may reasonably keep primitives because it exists for transport.

Not every string needs a class. A display label or a local loop counter gains nothing from wrapping. Introduce a type when a value has validation rules, a unit or format, or can be confused with another value of the same primitive type.

_Usage:_

"A refund went out at a hundred times the correct amount."

"One caller passed euros and the other expected cents. Let's replace that `number` with a `Money` type."

### Speculative generality

Speculative generality is code made flexible for future needs that have not arrived. Martin Fowler and Kent Beck listed it as a code smell in _Refactoring_ (1999). It is recognisable by interfaces with one implementation, parameters that every caller sets to the same value, abstract classes with one subclass, and plugin systems with one plugin. The felt symptom is tracing a one-line change through a factory, a provider and a strategy, then finding that only one path exists.

```typescript
// Built for many channels. Only email has ever existed.
interface NotificationChannel<TPayload, TOptions> {
  send(payload: TPayload, options?: TOptions): Promise<void>;
}

class NotificationChannelFactory {
  create(type: "email"): NotificationChannel<EmailPayload, EmailOptions> {
    return new EmailChannel();
  }
}

// What every caller needs.
async function sendEmail(to: string, subject: string, body: string) {}
```

The extra code must be read, tested and maintained from the day it is written. The prediction is also often wrong, so when the second case arrives it does not fit the prepared shape and the structure has to be reworked anyway. [YAGNI](#yagni) is the principle that addresses this directly.

Some flexibility is justified, and the cost of changing later is the deciding factor:

| Flexibility                         | Justified when                                         |
| ----------------------------------- | ------------------------------------------------------ |
| Interface with one production class | Tests use a second implementation, or the vendor may change |
| Extension point in a public library | Later changes would break consumers you do not control |
| Extra care in a data format         | Migrating stored data would be expensive               |
| Options on an internal helper       | Rarely; add them when a caller needs them              |

Decisions that are cheap to reverse can wait until the [last responsible moment](#last-responsible-moment).

This smell differs from [premature abstraction](#premature-abstraction). Premature abstraction merges existing code too early because it looks similar. Speculative generality adds capability for cases that do not exist.

To remove it, inline the single implementation, delete unused parameters and collapse hierarchies with one subclass. Version control keeps the old design if the need ever appears.

_Usage:_

"What does `NotificationChannelFactory` support?"

"Email. It has only ever supported email. Let's replace it with one function and add a second channel when we need one."

### Cargo cult programming

Cargo cult programming is copying code, patterns or practices without understanding why they work or whether they apply. The name draws on Richard Feynman's 1974 description of "cargo cult science", which used the image of Pacific islanders building imitation airstrips after the Second World War in the hope that cargo planes would return. In code, the symptoms include a `setTimeout(fn, 0)` nobody can explain, a `try/catch` around code that cannot throw, and the answer "it broke when I removed it" or "we always do it this way".

The habit appears at every level:

| Level        | Example                                  | Question to ask                         |
| ------------ | ---------------------------------------- | --------------------------------------- |
| Line         | An unexplained `sleep(200)`              | What race does this work around?        |
| Pattern      | A repository wrapping every ORM call     | What does this layer protect us from?   |
| Architecture | Microservices for a team of four         | Which constraint requires this?         |
| Process      | A daily meeting that informs no decision | What would change if we stopped?        |

The mechanism is copying the visible form of a practice without the conditions that made it work. A large company's architecture solves that company's scale and team structure. A [reference architecture](#reference-architecture) can be misused in the same way when adopted whole. Code pasted from a search result or generated by an assistant carries the same risk when it is merged without being read.

Before adopting a practice, state the problem it solves and how you would know it is working. Record the reasoning in a code comment or an [architecture decision record](#architecture-decision-record), so the next engineer can tell whether it still applies.

Understanding should also come before deletion. An unexplained line may be a genuine workaround for a production incident, so read its history or test without it on a branch first.

Cargo cult programming differs from a [golden hammer](#golden-hammer), where someone may understand a tool well and still overuse it. Following a team convention is also not a cargo cult when the team knows why the convention exists.

_Usage:_

"Why is there a `sleep(200)` before every database call?"

"Someone copied it from the old worker and nobody knows why. Let's find out what it was guarding against before we remove it."

### Premature abstraction

Premature [abstraction](#abstraction) is the extraction of a shared interface, helper or base class before enough real cases exist to show what they have in common. It usually starts with two similar blocks of code. Someone merges them, a third case differs slightly, and the shared function gains a flag. The symptom is a helper with parameters such as `isInvoice`, `hidePrice` and `legacy`, where a change for one caller breaks another.

```typescript
function renderCard(
  item: Item,
  opts: { compact?: boolean; isInvoice?: boolean; hidePrice?: boolean; legacy?: boolean },
) {
  if (opts.isInvoice && !opts.hidePrice) {
    // Invoice-only layout.
  }
  // Each new caller adds another flag and another branch.
}
```

The usual cause is applying [DRY](#dry) to similar-looking text instead of shared knowledge. Two validation rules can look identical today and change for different business reasons. Merging them creates [coupling](#coupling) between features that had no dependency. The wrong shared code can cost more than duplication, because changing it requires understanding every caller, and engineers tend to keep extending it once it exists.

The rule of three is a common heuristic: wait for three instances before extracting. It is a guide, and these questions are more precise:

| Question                                               | If yes        | If no         |
| ------------------------------------------------------ | ------------- | ------------- |
| Must a change to one case always apply to the others?  | Extract       | Keep separate |
| Can the shared part be named as one clear concept?     | Extract       | Keep separate |
| Would callers need flags to get different behaviour?   | Keep separate | Extract       |

To recover from a bad extraction, inline the shared code back into each caller and delete the branches that caller does not use. Then look at what remains and extract only what is common.

Premature abstraction differs from [speculative generality](#speculative-generality). Speculative generality builds for imagined future cases, while premature abstraction merges existing cases too early. Duplication is not always acceptable either: when the same business rule is copied and must stay identical, leaving it duplicated leads to [shotgun surgery](#shotgun-surgery).

_Usage:_

"I need `renderCard` on the invoice page, but it needs another flag."

"That would be the fifth flag. Copy the markup for invoices and we'll see what the two have in common."

### Inner-platform effect

The inner-platform effect is the tendency of a configurable system to grow into a poor copy of the platform it runs on. A table of generic `entity`, `attribute` and `value` rows rebuilds a database inside a database. A rules engine that gains conditions, variables and loops becomes a programming language with no debugger, tests or version control. The symptoms are a simple report that needs six self-joins, a configuration edit that takes down production and cannot be diffed, and a "no-code" tool that only one engineer can safely change.

| Inner platform                     | What it re-creates   | What is lost                               |
| ---------------------------------- | -------------------- | ------------------------------------------ |
| Entity-attribute-value tables      | Database schema      | Types, constraints, indexes, simple queries |
| YAML with conditions and loops     | Programming language | Type checking, debugger, tests             |
| Visual workflow builder            | Application code     | Diffs, code review, rollback               |
| Custom query language over SQL     | SQL                  | Query features, documentation, tooling     |
| Windowing system inside a web page | Browser or OS        | Accessibility, standard keyboard behaviour |

The effect develops through reasonable steps. To avoid a deployment, a team makes a value configurable. A later request needs a condition, and another needs a variable. Eventually the configuration requires an engineer to write it, and that engineer has fewer tools than the host language provided. The original motive is often [speculative generality](#speculative-generality) or a wish to let non-engineers make changes.

Prefer the platform's own features first. Limit configuration to values, and keep logic in code. If the reason for configuration is that deployment is slow, fixing deployment usually removes the need for it.

Some products do need an extension layer. A multi-tenant product where customers define their own fields needs some metadata model, and a [plugin architecture](#plugin-architecture) or the [interpreter pattern](#interpreter-pattern) can suit users outside the team who must extend the system. In those cases, treat the inner platform as a product, with validation, tests, versioning and documentation, and keep its scope deliberately small.

_Usage:_

"Can you change the discount rule in the workflow builder?"

"Nobody can debug it now that it has loops and variables. Let's move this rule back to code and ship it through CI."

### Not invented here

Not invented here is the tendency to reject an existing solution and build an in-house replacement, mainly because the solution came from outside the team or organisation. It is recognisable in a company that maintains its own authentication library, date parser, job queue and CSS framework, each with bugs that open-source projects fixed years ago. The engineer who wrote each one has often left, and new hires have to learn tools that exist nowhere else.

Writing the first version is usually a small part of the cost. The team also takes on security patches, documentation, onboarding and edge cases in areas such as time zones, Unicode and cryptography. That effort comes out of work on an organisation's [core domain](#core-domain), the part of the business that sets it apart. Generic [subdomains](#subdomain) such as email delivery or payments processing are usually better bought or adopted.

The decision depends on several factors:

| Factor             | Favours adopting                       | Favours building                       |
| ------------------ | -------------------------------------- | -------------------------------------- |
| Business relevance | Generic capability                     | Differentiates the product             |
| Fit                | Meets needs with small adaptations     | Requires heavy workarounds             |
| Risk area          | Security, cryptography, date handling  | Narrow, well-understood logic          |
| Project health     | Actively maintained                    | Abandoned or unmaintained              |
| Dependency size    | Proportionate to what you use          | Large package for one small function   |

The opposite failure is also a risk. Importing a large package for one function adds supply-chain exposure and upgrade work, and a few lines of well-understood code may be the better choice. Building can also be justified by licensing, latency or compliance requirements that no external option meets.

When adopting a dependency, limit how far it spreads. An [adapter](#adapter-pattern) or [anti-corruption layer](#anti-corruption-layer) keeps the vendor's types out of business code, so the dependency can be replaced later. Record the reasoning in an [architecture decision record](#architecture-decision-record), including what would cause the team to revisit it.

_Usage:_

"Our date library has handled daylight saving wrongly again."

"We wrote it years ago and nobody owns it. Let's move to a maintained library behind one small wrapper."
