---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2024-11-18
sr-due: 2025-11-22
sr-interval: 458
sr-ease: 230
archived: false
aliases:
  - DDD
---

# Domain Driven Design

https://docs.abp.io/en/abp/latest/Domain-Driven-Design

## Layers & Building Blocks

ABP follows DDD principles and patterns to achieve a layered application model which consists of four fundamental layers:

- **Presentation Layer**: Provides an interface to the user. Uses the _Application Layer_ to achieve user interactions.
- **Application Layer**: Mediates between the Presentation and Domain Layers. Orchestrates business objects to perform specific application tasks. Implements use cases as the application logic.
- **Domain Layer**: Includes business objects and the core (domain) business rules. This is the heart of the application.
- **Infrastructure Layer**: Provides generic technical capabilities that support higher layers mostly using 3rd-party libraries.

DDD mostly interest in the **Domain** and the **Application** layers, rather than the Infrastructure and the Presentation layers. The following documents explains the **infrastructure** provided by the ABP Framework to implement **Building Blocks** of the DDD:

- Domain Layer
	- [Entities & Aggregate Roots](Entities%20&%20Aggregate%20Roots.md)
	- [Repositories](Repositories.md)
	- [Domain Services](Domain%20Services.md)
	- [Value Objects](Value%20Objects.md)
	- [Specifications](Specifications.md)
- Application Layer
	- [Application Services](Application%20Services.md)
	- [[Data Transfer Objects]]
	- [Unit of Work](Unit%20of%20Work.md)

## Concepts

- [Domain](Domain.md): The subject area or business domain that the software is intended to support. It includes the business rules, entities, and processes

- [[Ubiquitous Language]]: A shared language between the technical team and the domain experts. It is used consistently in all communication and documentation, as well as in the code itself. This helps to ensure that everyone has a common understanding of the domain.

- Model: An abstract representation of the domain, focusing on the core business concepts and their relationships. The model is implemented in the code and reflects the ubiquitous language.

- Entities: Objects that have a distinct identity and lifecycle in the domain. They are defined by their identity rather than their attributes. For example, a User entity might have an ID, name, and email, but it is the ID that uniquely identifies the entity.

- Value Objects: Objects that are defined by their attributes and have no distinct identity. They are immutable and can be shared. For example, a Money value object might have a currency and amount.

- Aggregates: Clusters of associated objects that are treated as a unit for the purpose of data changes. Each aggregate has a root entity and a boundary that defines what is inside the aggregate. Changes to objects inside the aggregate boundary are made through the root entity.

- Repositories: Mechanisms for encapsulating storage, retrieval, and search behavior which emulate a collection of objects. They provide a way to access and persist aggregates.

- Factories: Mechanisms for encapsulating complex creation logic. They are used to create aggregates or other complex objects.

- Services: Operations or processes that don't naturally fit within the scope of an entity or value object. They are used to coordinate activities between different aggregates or to perform complex business logic.

- Bounded Contexts: Explicit boundaries within which a particular model is defined and applies. They help to divide a large system into coherent areas of responsibility and isolate different domain models.

- Context Mapping: The process of identifying and defining the relationships between different bounded contexts. It helps to manage the dependencies and interactions between different parts of the system.

- Anti-Corruption Layer (ACL): A layer that prevents the domain model from being corrupted by external influences, such as other bounded contexts or external systems. It translates requests and responses between the domain model and external systems.

- Domain Events: Events that capture changes in the domain model. They are used to propagate updates to other parts of the system and to trigger side effects.