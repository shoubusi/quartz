---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2023-12-13
sr-due: 2024-09-08
sr-interval: 171
sr-ease: 229
archived: false
---

# Entities & Aggregate Roots

https://docs.abp.io/en/abp/latest/Entities

An entity is generally mapped to a ==table== in a relational database.
<!--SR:!2024-03-20,6,229-->

## Entity Class

Entities are derived from the ==`Entity<TKey>`== class as shown below:
<!--SR:!2023-12-16,2,209-->

```csharp
public class Book : Entity<Guid>
{
    public string Name { get; set; }

    public float Price { get; set; }
}
```

> If you do not want to derive your entity from the base `Entity<TKey>` class, you can directly implement ==`IEntity<TKey>`== interface.
<!--SR:!2023-12-16,2,209-->

`Entity<TKey>` class just defines an `Id` property with the given primary **key type**, which is `Guid` in the example above. It can be other types like ==`string`, `int`, `long`, or whatever you need==.
<!--SR:!2023-12-17,3,229-->

### Entities with GUID Keys

If your entity's Id type is `Guid`, there are some good practices to implement:

- Create a constructor that gets the ==Id== as a parameter and passes to ==the base class==.
	- If you don't set a GUID Id, **ABP Framework sets it on save**, but it is good to have a valid Id on the entity even before saving it to the database.
- If you create an entity with a constructor that takes parameters, also create a ==`private` or `protected` empty constructor==. This is used while your database provider reads your entity from the database (on deserialization).
- Don't use the `Guid.NewGuid()` to set the Id! Use the ==`IGuidGenerator` service== while passing the Id from the code that creates the entity. `IGuidGenerator` optimized to generate sequential GUIDs, which is critical for clustered indexes in the relational databases. [[GUID Generation]]
<!--SR:!2023-12-16,2,209!2023-12-16,2,209!2023-12-16,2,209!2024-03-25,11,229-->

An example entity:

```csharp
public class Book : Entity<Guid>
{
    public string Name { get; set; }

    public float Price { get; set; }

    protected Book()
    {

    }

    public Book(Guid id)
     : base(id)
    {

    }
}
```

Example usage in an [application services](Application%20Services.md):
```csharp
public class BookAppService : ApplicationService, IBookAppService
{
    private readonly IRepository<Book> _bookRepository;

    public BookAppService(IRepository<Book> bookRepository)
    {
        _bookRepository = bookRepository;
    }

    public async Task CreateAsync(CreateBookDto input)
    {
        await _bookRepository.InsertAsync(
            new Book(GuidGenerator.Create())
            {
                Name = input.Name,
                Price = input.Price
            }
        );
    }
}
```
?
- `BookAppService` injects the default [repository](Repositories.md) for the book entity and uses its `InsertAsync` method to insert a `Book` to the database. ^30m218
- `GuidGenerator` is type of `IGuidGenerator` which is a property defined in the `ApplicationService` base class. ABP defines such frequently used base properties as pre-injected for you, so you don't need to manually inject them.
- If you want to follow the DDD best practices, see the _Aggregate Example_ section below.
<!--SR:!2024-03-25,11,249-->

### Entities with Composite Keys

Some entities may need to have **composite keys**. In that case, you can derive your entity from the non-generic `Entity` class. Example:

```csharp
public class UserRole : Entity
{
    public Guid UserId { get; set; }

    public Guid RoleId { get; set; }
    
    public DateTime CreationTime { get; set; }

    public UserRole()
    {
            
    }
    
    public override object[] GetKeys()
    {
        return new object[] { UserId, RoleId };
    }
}
```
?
For the example above, the composite key is composed of `UserId` and `RoleId`. For a relational database, it is the composite primary key of the related table. Entities with composite keys should implement the `GetKeys()` method as shown above.
<!--SR:!2023-12-29,4,209-->

> Notice that you also need to define keys of the entity in your **object-relational mapping** (ORM) configuration. See the [Entity Framework Core Integration](Entity%20Framework%20Core%20Integration.md) document for example.

> Also note that Entities with Composite Primary Keys cannot utilize the `IRepository<TEntity, TKey>` interface since it requires a single Id property. However, you can always use `IRepository<TEntity>`. See [repositories documentation](Repositories.md) for more.

### EntityEquals

`Entity.EntityEquals(...)` method is used to check if two Entity Objects are equals.

Example:

```csharp
Book book1 = ...
Book book2 = ...

if (book1.EntityEquals(book2)) //Check equality
{
    ...
}
```

## AggregateRoot Class

"_Aggregate is a pattern in Domain-Driven Design. A DDD aggregate is a cluster of domain objects that can be treated as a single unit. An example may be an order and its line-items, these will be separate objects, but it's useful to treat the order (together with its line items) as a single aggregate._" (see the [full description](http://martinfowler.com/bliki/DDD_Aggregate.html))

`AggregateRoot<TKey>` class ==extends== the `Entity<TKey>` class. So, it also has an `Id` property by default.
<!--SR:!2024-03-19,5,229-->

> Notice that ABP creates default repositories ==only for== aggregate roots ==by default==. However, it's possible to include all entities. See the [repositories documentation](Repositories.md) for more.
<!--SR:!2024-03-21,7,229!2024-03-20,6,229-->

ABP does not force you to use aggregate roots, you can in fact use the `Entity` class as defined before. However, if you want to implement the [Domain Driven Design](https://docs.abp.io/en/abp/latest/Domain-Driven-Design) and want to create aggregate root classes, there are some best practices you may want to consider:

- An aggregate root is responsible to preserve it's own integrity. This is also true for all entities, but aggregate root has responsibility for ==it's sub entities== too. So, the aggregate root must always be in a valid state.
- An aggregate root can be referenced by it's Id. ==Do not reference it by it's navigation property.==
- An aggregate root is treated as a ==single== unit. It's retrieved and updated as a ==single== unit. It's generally considered as a transaction ==boundary==.
- Work with sub-entities over the aggregate root, do not modify them independently.
<!--SR:!2023-12-17,3,236!2023-12-16,2,209!2024-03-19,5,229!2024-03-23,9,256-->

See the [entity design best practice guide](https://docs.abp.io/en/abp/latest/Best-Practices/Entities) if you want to implement DDD in your application.

> [!question] to implement DDD, when to use Entity, and when to use AggregateRoot
> In [[Domain Driven Design]],  use an Entity when an object's identity is important and needs to be tracked independently. 
> Use[](Domain%20Driven%20Design.md)a group of objects need to be treated as a single unit for consistency and transactional boundaries.
> An Aggregate Root acts as a boundary for its contained Entities and controls their lifecycle.


### Aggregate Example

This is a full sample of an aggregate root with a related sub-entity collection:

```csharp
public class Order : AggregateRoot<Guid>
{
    public virtual string ReferenceNo { get; protected set; }

    public virtual int TotalItemCount { get; protected set; }

    public virtual DateTime CreationTime { get; protected set; }

    public virtual List<OrderLine> OrderLines { get; protected set; }

    protected Order()
    {

    }

    public Order(Guid id, string referenceNo)
    {
        Check.NotNull(referenceNo, nameof(referenceNo));
        
        Id = id;
        ReferenceNo = referenceNo;
        
        OrderLines = new List<OrderLine>();
    }

    public void AddProduct(Guid productId, int count)
    {
        if (count <= 0)
        {
            throw new ArgumentException(
                "You can not add zero or negative count of products!",
                nameof(count)
            );
        }

        var existingLine = OrderLines.FirstOrDefault(ol => ol.ProductId == productId);

        if (existingLine == null)
        {
            OrderLines.Add(new OrderLine(this.Id, productId, count));
        }
        else
        {
            existingLine.ChangeCount(existingLine.Count + count);
        }

        TotalItemCount += count;
    }
}

public class OrderLine : Entity
{
    public virtual Guid OrderId { get; protected set; }

    public virtual Guid ProductId { get; protected set; }

    public virtual int Count { get; protected set; }

    protected OrderLine()
    {

    }

    internal OrderLine(Guid orderId, Guid productId, int count)
    {
        OrderId = orderId;
        ProductId = productId;
        Count = count;
    }

    internal void ChangeCount(int newCount)
    {
        Count = newCount;
    }
    
    public override object[] GetKeys()
    {
        return new Object[] {OrderId, ProductId};
    }
}
```

> If you do not want to derive your aggregate root from the base `AggregateRoot<TKey>` class, you can directly implement the ==`IAggregateRoot<TKey>`== interface.
<!--SR:!2023-12-16,2,209-->

`Order` is an **aggregate root** with `Guid` type `Id` property. It has a collection of `OrderLine` entities. `OrderLine` is another entity with a composite primary key (`OrderId` and `ProductId`).

While this example may not implement all the best practices of an aggregate root, it still follows some good practices:

- `Order` has a public constructor that takes ==**minimal requirements**== to construct an `Order` instance. So, it's not possible to create an order without an id and reference number. The **protected/private** constructor is only necessary to **deserialize** the object while reading from a data source.
- `OrderLine` constructor is internal, so it is only allowed to be created by the domain layer. It's used inside of the `Order.AddProduct` method.
- `Order.AddProduct` implements the business rule to add a product to an order.
- All properties have `protected` setters. This is to prevent the entity from arbitrary changes from outside of the entity. For example, it would be dangerous to set `TotalItemCount` without adding a new product to the order. It's value is maintained by the `AddProduct` method.
<!--SR:!2023-12-17,3,229-->

ABP Framework does not force you to apply any DDD rule or patterns. However, it tries to make it possible and easier when you do want to apply them. The documentation also follows the same principle.

### Aggregate Roots with Composite Keys

While it's not common (and not suggested) for aggregate roots, it is in fact possible to define composite keys in the same way as defined for the mentioned entities above. Use non-generic `AggregateRoot` base class in that case.

### BasicAggregateRoot Class

`AggregateRoot` class implements the `IHasExtraProperties` and `IHasConcurrencyStamp` interfaces which brings two properties to the derived class. `IHasExtraProperties` makes the entity extensible (see the _Extra Properties_ section below) and `IHasConcurrencyStamp` adds a `ConcurrencyStamp` property that is managed by the ABP Framework to implement the [optimistic concurrency](https://docs.microsoft.com/en-us/ef/core/saving/concurrency). In most cases, these are wanted features for aggregate roots.

However, if you don't need these features, you can inherit from the `BasicAggregateRoot<TKey>` (or `BasicAggregateRoot`) for your aggregate root.

## Base Classes & Interfaces for Audit Properties

There are some properties like `CreationTime`, `CreatorId`, `LastModificationTime`... which are very common in all applications. ABP Framework provides some interfaces and base classes to **standardize** these properties and also **sets their values automatically**.

### Auditing Interfaces

There are a lot of auditing interfaces, so you can implement the one that you need.

> While you can manually implement these interfaces, you can use **the base classes** defined in the next section to simplify it.

Once you implement any of the interfaces, or derive from a class defined in the next section, ABP Framework ==automatically== manages these properties wherever possible.
<!--SR:!2023-12-17,3,236-->

Implementing `ISoftDelete`, `IDeletionAuditedObject` or `IFullAuditedObject` makes your entity ==**soft-delete**==. See the [data filtering document](Data%20Filtering.md) to learn about the soft-delete pattern.
<!--SR:!2023-12-16,2,209-->

### Auditing Base Classes

While you can manually implement any of the interfaces defined above, it is suggested to inherit from the base classes defined here:

- `CreationAuditedEntity<TKey>` and `CreationAuditedAggregateRoot<TKey>` implement the `ICreationAuditedObject` interface.
- `AuditedEntity<TKey>` and `AuditedAggregateRoot<TKey>` implement the `IAuditedObject` interface.
- `FullAuditedEntity<TKey>` and `FullAuditedAggregateRoot<TKey>` implement the `IFullAuditedObject` interface.

All these base classes also have non-generic versions to take `AuditedEntity` and `FullAuditedAggregateRoot` to support the composite primary keys.

All these base classes also have `...WithUser` pairs, like `FullAuditedAggregateRootWithUser<TUser>` and `FullAuditedAggregateRootWithUser<TKey, TUser>`. This makes possible to add a navigation property to your user entity. However, it is not a good practice to add navigation properties between aggregate roots, so this usage is not suggested (unless you are using an ORM, like EF Core, that well supports this scenario and you really need it - otherwise remember that this approach doesn't work for NoSQL databases like MongoDB where you must truly implement the aggregate pattern). Also, if you add navigation properties to the AppUser class that comes with the startup template, consider to handle (ignore/map) it on the migration dbcontext (see [the EF Core migration document](https://docs.abp.io/en/abp/latest/Entity-Framework-Core-Migrations)).

## Caching Entities

ABP Framework provides a [Distributed Entity Cache System](https://docs.abp.io/en/abp/latest/Entity-Cache) for caching entities. It is useful if you want to use caching for quicker access to the entity rather than repeatedly querying it from the database.

It's designed as read-only and automatically invalidates a cached entity if the entity is updated or deleted.

> See the [Entity Cache](https://docs.abp.io/en/abp/latest/Entity-Cache) documentation for more information.

## Versioning Entities

ABP defines the `IHasEntityVersion` interface for automatic versioning of your entities. It only provides a single ==`EntityVersion`== property, as shown in the following code block:
<!--SR:!2023-12-17,3,236-->

```csharp
public interface IHasEntityVersion
{
    int EntityVersion { get; }
}
```

If you implement the `IHasEntityVersion` interface, ABP automatically increases the `EntityVersion` value whenever ==you update your entity==. The initial `EntityVersion` value will be `0`, when you first create an entity and save to the database.
<!--SR:!2023-12-16,2,209-->

> ABP can not increase the version if you directly execute SQL `UPDATE` commands in the database. It is your responsibility to increase the `EntityVersion` value in that case. Also, if you are using the aggregate pattern and change sub-collections of an aggregate root, it is your responsibility if you want to increase the version of the aggregate root object.

## Extra Properties

ABP defines the `IHasExtraProperties` interface that can be implemented by an entity to be able to ==dynamically set and get properties== for the entity. `AggregateRoot` base class already implements the `IHasExtraProperties` interface. If you've derived from this class (or one of the related audit class defined above), you can directly use the API.
<!--SR:!2024-03-16,1,196-->

