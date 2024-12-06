---
date created: 2024-06-28
date modified: 2024-07-01
tags: knowledge
archived: false
---

# Nullable reference types

[wucai-2024-07-01-H8EDAB8](../WuCai/2024/07/wucai-2024-07-01-H8EDAB8.md)

https://learn.microsoft.com/en-us/dotnet/csharp/nullable-references
https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-reference-types

- [null-coalescing operator](null-coalescing%20operator.md)
- [null-forgiving operator](null-forgiving%20operator.md)
- [null-conditional operator](null-conditional%20operator.md)



in csharp syntax, what does a question mark(?) after a type name mean

A question mark (`?`) after a type name in C# is called the nullable operator. It indicates that the variable of that type can be either null or an instance of the specified type.

For example:

```csharp
int? nullableInteger;
```

In this case, `nullableInteger` can be either `null` or an integer value. If you try to assign a null value to it without checking if it's already null, you'll get a compile-time error.

Here are some key points about the nullable operator:

1. **Nullability**: The question mark after the type name indicates that the variable can be null.
2. **Default Value**: The default value of a nullable type is `null`.
3. **Implicit Conversion**: You can implicitly convert between a non-nullable and a nullable version of the same type (e.g., from `int` to `int?`, or vice versa).
4. **Null Check**: When you access a nullable property, you need to perform null checks before using its value.

The nullable operator is useful when working with variables that can be either present or absent in your code.

```csharp
// Example 1: Checking for null values

string? name = null; // Declares a string variable 'name' as nullable

Console.WriteLine($"Name is: {name ?? "Unknown"}"); // Prints "Name is: Unknown" if 'name' is null, otherwise prints the value of 'name'.

// Example 2: Providing default values for nullable types

int? age = null;
string message = $"Welcome, {age.HasValue ? $"user aged {age}" : "user"}!";

// Example 3: Using a nullable type to store the result of a query

public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public DateTime? BirthDate { get; set; } // Nullable property for storing birthdate, which may be null.

}

// ... (later in your code)

var user = dbContext.Users.FirstOrDefault(u => u.Id == 1); // Get the first user from the database
int? userId = user?.Id ?? -1;
```

