---
status: closed
tags:
  - Node
  - knowledge
type: Node
archived: false
---

# Anonymous types

The article from Microsoft Learn provides an in-depth look at anonymous types in C#. Here is a summary of the key points:

1. **Definition and Creation**: Anonymous types are a convenient way to create objects with a set of read-only properties without explicitly defining a class or struct. They are created using the `new` operator with an object initializer.

2. **Property Inference**: The type of each property in an anonymous type is inferred by the compiler, and the type name is generated and not available at the source code level.

3. **Usage in Queries**: Anonymous types are commonly used in the `select` clause of LINQ queries to return a subset of properties from each object in the source sequence.

4. **Properties**: Anonymous types can have one or more public read-only properties but cannot contain methods, events, or any other class members.

5. **Initialization from Other Types**: Properties from existing types can be used to initialize an anonymous type. If member names are not specified, the compiler uses the property names from the source.

6. **IDE Support**: The .NET style rule IDE0037 can enforce the preference for inferred or explicit member names.

7. **Nested Anonymous Types**: It's possible to define a field in an anonymous type using an object of another type, including classes, structs, or even another anonymous type.

8. **Implicit Typing**: Variables of anonymous types are typically declared using `var` since the type name is not accessible to the developer.

9. **Arrays of Anonymous Types**: You can create an array of elements with anonymous types, combining an implicitly typed local variable with an implicitly typed array.

10. **Type Information**: Anonymous types are class types that derive from `object`. The compiler provides a unique name for each type, but this name is not accessible to the application.

11. **Equality and Hash Code**: The `Equals` and `GetHashCode` methods are defined based on the properties' `Equals` and `GetHashCode` methods, meaning two instances are equal only if all their properties are equal.

12. **Accessibility**: Anonymous types have an `internal` accessibility level, meaning types defined in different assemblies are considered different, even if their properties are the same.

13. **ToString Method**: Anonymous types override the `ToString` method to provide a string representation that includes the property names and values within curly braces.

14. **Feedback and Contributions**: The content is open for collaboration on GitHub, where issues and pull requests can be created and reviewed.

The article is a comprehensive guide to understanding and using anonymous types in C#, providing examples and best practices for developers.
