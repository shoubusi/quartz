---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2024-04-25
sr-due: 2026-09-04
sr-interval: 694
sr-ease: 263
archived: false
---

# Application Services

https://docs.abp.io/en/abp/latest/Application-Services

Application services are used to implement the **use cases** of an application. They are used to **expose domain logic to the presentation layer**.

An Application Service is called from the presentation layer (optionally) with a [DTO](Data%20Transfer%20Objects.md) as the parameter. It uses domain objects to **perform some specific business logic** and (optionally) returns a DTO back to the presentation layer. Thus, the presentation layer is completely **isolated** from domain layer.

- [Application Services vs Domain Services](Domain%20Services.md#Application%20Services%20vs%20Domain%20Services)
- [Application Services Best Practices](Application%20Services%20Best%20Practices.md)



IApplicationService

```csharp
public interface IBookAppService : IApplicationService
{
    Task CreateAsync(CreateBookDto input);
}
```

Implementation
