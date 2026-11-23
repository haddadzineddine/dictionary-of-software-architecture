---
description: A way of diagramming software at four zoom levels, from system context down to containers, components and code.
---

The C4 model is a way of diagramming [software architecture](./Software%20architecture.md) at four levels of zoom: context, containers, components and code. Simon Brown created it. Each level answers a different question for a different audience, in the way a map can zoom from a country to a street.

It addresses diagrams that cannot be read without their author. A whiteboard photo with unlabelled boxes and arrows may mix a database, a team, a Kubernetes cluster and a class at the same level, and two engineers will interpret it differently.

| Level             | Shows                                                    | Audience                     |
| ----------------- | -------------------------------------------------------- | ---------------------------- |
| 1. System context | The system, its users and external systems               | Everyone, including non-technical people |
| 2. Container      | Separately running units and how they communicate        | Engineers, operations        |
| 3. Component      | Major building blocks inside one container               | Engineers working on it      |
| 4. Code           | Classes or functions in one component                    | Rarely drawn by hand         |

A container in C4 is not a Docker container. It means something that must be running for the system to work, such as a web app, an API, a database or a message broker.

The model does not prescribe a notation. It asks that each element has a name, type, technology and short description, and that each arrow has a label saying what the relationship does. "Sends order events to" is more informative than an unlabelled line.

Levels 1 and 2 are enough for many teams. Level 3 helps with complex containers, and level 4 is usually generated from code or omitted because it goes stale quickly. Keeping diagrams as code in the repository, with a tool such as Structurizr or Mermaid, means they are reviewed alongside changes and reduces [architectural drift](./Architectural%20drift.md) between the diagram and the system. C4 describes structure only, so pair it with an [architecture decision record](./Architecture%20decision%20record.md) to explain why that structure exists.

_Usage:_

"Is this box on the diagram a service, a database or a team?"

"Redraw it as a C4 container diagram and label every box and arrow."
