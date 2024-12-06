---
# Mandatory fields
id: "d05714dc-13bb-4110-88c0-72e5da532076"
# Optional fields
title: "Record keyword"
tags: []
source: ""
source_title: ""
source_description: ""
source_image_url: ""
created_date: "2024-11-19"
modified_date: "2024-11-19"
deleted: true
---
In C#, the `record` keyword is used to define a reference type that provides built-in functionality for encapsulating data. Records are particularly useful for creating immutable data structures, where the data is intended to be read-only after initialization. They are often used for data transfer objects (DTOs), value objects, and other scenarios where immutability and value-based equality are desirable.

Here are some key features and usages of the `record` keyword in C#:

### 1. **Immutability**
Records are immutable by default, meaning that once an instance is created, its properties cannot be changed. This is achieved through the use of `init` accessors instead of `set` accessors.

```csharp
public record Person(string FirstName, string LastName);

var person = new Person("John", "Doe");
// person.FirstName = "Jane"; // This would cause a compile-time error
```

### 2. **Value-Based Equality**
Records provide value-based equality semantics, meaning that two instances of a record are considered equal if their properties are equal. This is in contrast to reference-based equality, where two instances are considered equal only if they refer to the same object in memory.

```csharp
var person1 = new Person("John", "Doe");
var person2 = new Person("John", "Doe");

Console.WriteLine(person1 == person2); // True
```

### 3. **Deconstruction**
Records support deconstruction, allowing you to easily extract the properties of a record into separate variables.

```csharp
var person = new Person("John", "Doe");
var (firstName, lastName) = person;

Console.WriteLine(firstName); // John
Console.WriteLine(lastName); // Doe
```

### 4. **With Expressions**
Records support `with` expressions, which allow you to create a new instance of a record with some properties modified. This is useful for creating modified copies of immutable records.

```csharp
var person = new Person("John", "Doe");
var updatedPerson = person with { FirstName = "Jane" };

Console.WriteLine(updatedPerson.FirstName); // Jane
```

### 5. **Inheritance**
Records can inherit from other records, allowing you to create a hierarchy of immutable data structures.

```csharp
public record Person(string FirstName, string LastName);
public record Employee(string FirstName, string LastName, string EmployeeId) : Person(FirstName, LastName);

var employee = new Employee("John", "Doe", "E123");
```

### 6. **Positional and Nominal Syntax**
Records can be defined using positional syntax (similar to tuples) or nominal syntax (similar to classes).

```csharp
// Positional syntax
public record Person(string FirstName, string LastName);

// Nominal syntax
public record Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}
```

### 7. **Sealed Records**
You can create sealed records to prevent inheritance, ensuring that the record cannot be extended.

```csharp
public sealed record Person(string FirstName, string LastName);
```

### Example Usage
Here is a complete example that demonstrates some of the features of records:

```csharp
using System;

public record Person(string FirstName, string LastName);

public class Program
{
    public static void Main()
    {
        var person1 = new Person("John", "Doe");
        var person2 = new Person("John", "Doe");

        Console.WriteLine(person1 == person2); // True

        var (firstName, lastName) = person1;
        Console.WriteLine($"{firstName} {lastName}"); // John Doe

        var updatedPerson = person1 with { FirstName = "Jane" };
        Console.WriteLine(updatedPerson.FirstName); // Jane
    }
}
```

In summary, the `record` keyword in C# is a powerful feature for creating immutable data structures with value-based equality, deconstruction, and other useful features. It simplifies the creation of data transfer objects and other scenarios where immutability is beneficial.



https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/records

[Differences and Scenarios Record and Struct](Differences%20and%20Scenarios%20Record%20and%20Struct.md)