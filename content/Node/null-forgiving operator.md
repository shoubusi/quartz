---
date created: 2024-06-28
date modified: 2024-07-02
tags: knowledge
archived: false
---

# null-forgiving operator

explain the exclamation mark in following csharp code

```
public required string Message { get; set; } = null!;
```

The `null!` syntax at the end of the assignment is used to indicate that a non-nullable reference type can be assigned a value of `null`.

In C# 11, which was released in 2021, Microsoft introduced nullable reference types. A reference type (like a string) can either be nullable or not nullable.

When you declare a property like this:

```csharp
public required string Message { get; set; } = null;
```

You are declaring that the `Message` property is not nullable. This means that when you assign a value to it, you must ensure that it's never going to be `null`. 

However, when you declare a property like this:

```csharp
public required string Message { get; set; } = null!;
```

You are explicitly stating that the property can be assigned `null`, even though it was declared as not nullable. The exclamation mark at the end of the assignment is what does this.

This syntax tells the compiler: "I know you think I'm trying to assign a value to a non-nullable reference type, but in reality, I want that property to be `null`. So please just ignore your own rules and let me do it."

In other words, `null!` is used when you need to explicitly indicate that the compiler should not throw an error about assigning null to a non-nullable reference type.

https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-forgiving
