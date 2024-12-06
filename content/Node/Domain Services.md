---
date created: 2023-11-16
date modified: 2024-03-28
tags:
  - review
  - ABP
  - knowledge
sr-due: 2025-12-19
sr-interval: 485
sr-ease: 244
archived: false
---

# Domain Services

[Domain Services](https://docs.abp.io/en/abp/latest/Domain-Services) 
[Domain Services Best Practices](Domain%20Services%20Best%20Practices.md)

## Application Services vs Domain Services

In Domain-Driven Design (DDD), Application Services and Domain Services serve different purposes:

1. **Application Services**: Application Services are responsible for coordinating tasks and acting as an interface between the presentation layer and the domain layer. They orchestrate the execution of domain logic by interacting with domain objects and coordinating multiple domain services. Application Services are typically [stateless](stateless.md) and focus on high-level operations that are meaningful to the application as a whole.

2. **Domain Services**: Domain Services, on the other hand, encapsulate domain logic that doesn't naturally fit within a single entity or value object. They represent operations or behaviors that involve multiple entities or don't belong to any specific entity. Domain Services are part of the domain layer and are designed to enforce business rules and ensure proper behavior within the domain model.

In summary, Application Services focus on application-level operations and serve as an entry point to the domain layer, while Domain Services encapsulate domain-specific logic that doesn't belong to any single entity.

---

While both of [Application Services](https://docs.abp.io/en/abp/latest/Application-Services) and Domain Services implement the business rules, there are fundamental logical and formal differences;

- Application Services implement the **use cases** of the application (user interactions in a typical web application), while Domain Services implement the **core, use case independent domain logic**.
- Application Services get/return [Data Transfer Objects](https://docs.abp.io/en/abp/latest/Data-Transfer-Objects), Domain Service methods typically get and return the **domain objects** ([entities](https://docs.abp.io/en/abp/latest/Entities), [value objects](https://docs.abp.io/en/abp/latest/Value-Objects)).
- Domain services are typically used by the Application Services or other Domain Services, while Application Services are used by the Presentation Layer or Client Applications.

---
Scenarios

In Domain-Driven Design (DDD), domain services are used to encapsulate domain logic that does not naturally fit within an entity or value object. Domain services are stateless and operate on multiple entities or value objects to perform a specific operation.

You should consider using a domain service in the following scenarios:

1. **Cross-aggregate operations**: When an operation involves multiple aggregates and cannot be owned by a single aggregate root.
  
2. **Complex business logic**: When the logic is complex and doesn't naturally belong to any specific entity or value object.
  
3. **External dependencies**: When the operation requires interaction with external systems or services.
  
4. **Reusability**: When the same logic needs to be reused across multiple entities.

Remember that domain services should be designed in a way that they are cohesive and follow the Single Responsibility Principle. They should only contain business logic related to the domain and should not have any infrastructure concerns.