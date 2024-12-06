---
date created: 2024-12-02
date modified: 2024-12-02
---

# Differences and Scenarios Record and Struct

In C#, both `record` and `struct` are used to define types, but they serve different purposes and have distinct characteristics. Here's a breakdown of the differences and scenarios where you might use each:

## Records

### Characteristics

1. **Reference Type**: Records are reference types, meaning they are allocated on the heap and compared by reference by default.
2. **Immutability**: Records are designed to be immutable by default, although you can create mutable records if needed.
3. **Value Equality**: Records provide built-in value equality, meaning two records are considered equal if all their properties are equal.
4. **Concise Syntax**: Records offer a concise syntax for defining data-carrying types, especially with `record` positional syntax.
5. **Inheritance**: Records support inheritance, allowing you to create hierarchies of records.

### Scenarios

- **Data Models**: When you need a data model with value equality and immutability.
- **DTOs**: When transferring data between layers or systems, especially when you want to ensure immutability.
- **Pattern Matching**: Records work well with pattern matching due to their value equality.

### Example

```csharp
public record Person(string FirstName, string LastName);
```

## Structs

### Characteristics

1. **Value Type**: Structs are value types, meaning they are allocated on the stack (or inline in arrays) and compared by value.
2. **Mutability**: Structs are mutable by default, although they can be made immutable by using `readonly` fields.
3. **No Inheritance**: Structs do not support inheritance (except for implementing interfaces).
4. **Performance**: Structs can offer performance benefits due to stack allocation, especially for small, short-lived objects.
5. **Default Constructor**: Structs have an implicit parameterless constructor that initializes fields to their default values.

#### Scenarios

- **Small Data Structures**: When you need a small, simple data structure that benefits from stack allocation.
- **Performance-Critical Code**: When performance is critical, and you want to avoid heap allocations.
- **Interoperability**: When working with unmanaged code or APIs that require value types.

#### Example

```csharp
public struct Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```

## Key Differences Summary

1. **Type**:
   - **Record**: Reference type
   - **Struct**: Value type

2. **Equality**:
   - **Record**: Value equality by default
   - **Struct**: Value equality, but must implement `IEquatable<T>` for custom equality

3. **Immutability**:
   - **Record**: Immutable by default
   - **Struct**: Mutable by default

4. **Inheritance**:
   - **Record**: Supports inheritance
   - **Struct**: No inheritance

5. **Performance**:
   - **Record**: Heap allocation
   - **Struct**: Stack allocation

6. **Use Cases**:
   - **Record**: Data models, DTOs, pattern matching
   - **Struct**: Small data structures, performance-critical code, interoperability

Choose `record` when you need a reference type with value semantics and immutability, and choose `struct` when you need a lightweight value type for performance reasons.
