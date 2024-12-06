---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2024-12-02
sr-due: 2026-02-25
sr-interval: 553
sr-ease: 266
archived: false
---

# Value Objects

[Value Objects](https://docs.abp.io/en/abp/latest/Value-Objects)

> An object that represents a descriptive aspect of the domain with no conceptual identity is called a VALUE OBJECT.
> 
> (Eric Evans)

Two [Entities](https://docs.abp.io/en/abp/latest/Entities) with the same properties but with different `Id`s are considered as different entities. However, Value Objects have no `Id`s and they are considered as equals if they have the same property values.

## The ValueObject Class in ABP

`ValueObject` is an abstract class that can be inherited to create a Value Object class.

**Example: An Address class**

```csharp
public class Address : ValueObject
{
    public Guid CityId { get; private set; }

    public string Street { get; private set; }

    public int Number { get; private set; }

    private Address()
    {
        
    }
    
    public Address(
        Guid cityId,
        string street,
        int number)
    {
        CityId = cityId;
        Street = street;
        Number = number;
    }

    protected override IEnumerable<object> GetAtomicValues()
    {
        yield return Street;
        yield return CityId;
        yield return Number;
    }
}
```

- A Value Object class must implement the `GetAtomicValues()` method to return the primitive values.

### ValueEquals

`ValueObject.ValueEquals(...)` method is used to check if two Value Objects are equals.

**Example: Check if two addresses are equals**

```csharp
Address address1 = ...
Address address2 = ...

if (address1.ValueEquals(address2)) //Check equality
{
    ...
}
```

## Best Practices

Here are some best practices when using Value Objects:

- Design a value object as ==**immutable**== (like the Address above) if there is not a good reason for designing it as mutable.
- The properties that make up a Value Object should form ==a conceptual whole==. For example, CityId, Street and Number shouldn't be separate properties of a Person entity. This also makes the Person entity simpler.

Let me explain Value Objects in Domain-Driven Design (DDD).

## Value Objects in DDD

A Value Object is one of the fundamental building blocks in DDD, alongside Entities and Aggregates. Here are the key characteristics and scenarios for using Value Objects:

### Key Characteristics

1. **Immutable**: Once created, they cannot be changed
2. **No Identity**: They are compared by their attributes, not by an ID
3. **Equality based on attributes**: Two value objects with the same properties are considered equal
4. **Self-validating**: They ensure their own consistency

### Common Scenarios for Value Objects

1. **Measurements and Quantities**
```csharp
public record Money
{
    public decimal Amount { get; init; }
    public string Currency { get; init; }

    public Money(decimal amount, string currency)
    {
        if (amount < 0) throw new ArgumentException("Amount cannot be negative");
        Amount = amount;
        Currency = currency;
    }
}
```

2. **Addresses**
```csharp
public record Address
{
    public string Street { get; init; }
    public string City { get; init; }
    public string PostalCode { get; init; }
    public string Country { get; init; }
}
```

3. **Date Ranges**
```csharp
public record DateRange
{
    public DateTime Start { get; init; }
    public DateTime End { get; init; }

    public DateRange(DateTime start, DateTime end)
    {
        if (end < start) throw new ArgumentException("End date must be after start date");
        Start = start;
        End = end;
    }

    public bool Contains(DateTime date) => date >= Start && date <= End;
}
```

### Benefits

- **Encapsulates Business Rules**: Value objects can contain validation and business rules
- **Prevents Primitive Obsession**: Instead of using primitive types, you create meaningful domain concepts
- **Improves Code Clarity**: Makes the code more expressive and self-documenting
- **Ensures Consistency**: Business rules are enforced at creation

### Example in Context

```csharp
public class Order
{
    public OrderId Id { get; private set; }
    public Money Price { get; private set; }
    public Address ShippingAddress { get; private set; }
    public DateRange DeliveryWindow { get; private set; }
}
```

In this example, `Money`, `Address`, and `DateRange` are all value objects that help make the `Order` entity more meaningful and enforce business rules at a granular level.

Remember: If you need to track identity or lifecycle, use an Entity. If you only care about the attributes and their values, use a Value Object.

[Value Objects Vs DTOs in Scenario](Node/Value%20Objects%20Vs%20DTOs%20in%20Scenario.md)
