---
date created: 2024-03-27
date modified: 2024-03-28
tags:
  - ABP
  - knowledge
archived: false
---
Module Architecture For WPF



- **Domain Layer**:
	- **Domain.Shared package**: Contains constants, enums and other types those can be safely shared with the all layers of the module.
		- constants
		- enums
	- **Domain package**: Contains entities, repository ==interfaces==, domain service ==interfaces== and ==their implementations== and other domain objects.
		- [Entities & Aggregate Roots](Entities%20&%20Aggregate%20Roots.md)
			- `Entity<Guid>` and `AggregateRoot<Guid>`
			- `CreationAuditedEntity<TKey>` and `CreationAuditedAggregateRoot<TKey>` implement the `ICreationAuditedObject` interface.
			- `AuditedEntity<TKey>` and `AuditedAggregateRoot<TKey>` implement the `IAuditedObject` interface.
			- `FullAuditedEntity<TKey>` and `FullAuditedAggregateRoot<TKey>` implement the `IFullAuditedObject` interface.
		- [Value Objects](Value%20Objects.md)
			- `ValueObject`
		- [Repositories](Repositories.md)
			- `IRepository<TEntity, TKey>`
			- `IBasicRepository<TEntity, TPrimaryKey>` and `IBasicRepository<TEntity>`
			- `IReadOnlyRepository<TEntity, TKey>` and `IReadOnlyBasicRepository<Tentity, TKey>`
		- [Domain Services](Domain%20Services.md)
			- `DomainService`
		- [[Specifications]]
			- `Specification<T>`
- **Application Layer**:
	- **Application.Contracts package**: Contains application service interfaces and DTOs (Data Transfer Objects) that define the contract between the application layer and the domain layer.
		- [Application Services](Application%20Services.md) interfaces
			- `IApplicationService`
			- `ICrudAppService`
		- [DTO](Data%20Transfer%20Objects.md)
			- `EntityDto<TKey>`
			- `FullAuditedEntityDto`
			- `ListResultDto<T>` and `IListResult<T>`
				- Request
					- `LimitedResultRequestDto` implements `ILimitedResultRequest`.
					- `PagedResultRequestDto` implements `IPagedResultRequest` (and inherits from the `LimitedResultRequestDto`).
					- `PagedAndSortedResultRequestDto` implements `IPagedAndSortedResultRequest` (and inherit from the `PagedResultRequestDto`).
				- Response
					- `PagedResultDto<T>` inherits from the `ListResultDto<T>` and also implements the `IPagedResult<T>`.
		- [Unit of Work](Unit%20of%20Work.md)
	- **Application package**: Contains application services that orchestrate the domain logic, handle application-specific operations, and interact with the domain layer.
		- [Application Services](Application%20Services.md) implementations
			- `ApplicationService`
			- `CrudAppService`
- **Infrastructure Layer**:
	- **Entity Framework Core**: Contains database context, entity configurations, repositories implementations, and other infrastructure-related code that interacts with the database.
- **Presentation Layer**:
	- **WPF Application**: Contains the user interface components, views, view models, and other presentation-related code that interacts with the application layer to provide a user-friendly interface for the application.
