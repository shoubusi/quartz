---
status: closed
tags:
  - Node
  - knowledge
type: Node
archived: false
---
# Generic classes and methods


https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics

The provided resource from Microsoft's website is an article about generic classes and methods in C#. Here's a summary of the key points:

1. **Generics Overview**: Generics are a feature in .NET that allow for the creation of classes and methods with type parameters. This means you can write code that is type-safe and efficient without specifying the exact data type until the class or method is used.

2. **Usage of Generics**: They are commonly used in collections and the `System.Collections.Generic` namespace provides several generic collection classes. Non-generic collections like `ArrayList` are maintained for compatibility but are not recommended.

3. **Creating Custom Generics**: You can create your own generic types and methods to provide generalized solutions that are type-safe and efficient. An example is provided of a simple generic linked-list class.

4. **Type Parameters**: The type parameter `T` is used in various places in the generic class to indicate the type of the item stored in the list. When a generic class is instantiated with a concrete type, each occurrence of `T` is replaced with that type.

5. **Generic Interfaces and Structs**: Generics are not limited to classes; you can also define generic interfaces and structs, including record types.

6. **Benefits of Generics**: They maximize code reuse, enhance type safety, and improve performance. Generic collections should be used over non-generic ones whenever possible.

7. **Constraints and Reflection**: Generic classes can be constrained to access methods on specific data types. Information about the types used in a generic data type can be obtained at runtime using reflection.

