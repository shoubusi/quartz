---
status: closed
tags:
  - Node
  - knowledge
type: Node
archived: false
---

# Interfaces - define behavior for multiple types

https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces


The article from Microsoft Learn titled "Interfaces - define behavior for multiple types" provides an in-depth look at how interfaces are used in C# to define a contract for related functionalities that classes or structs must implement. Here's a summary of the key points:

1. **Purpose of Interfaces**: Interfaces outline a set of functionalities that implementing classes or structs must provide. They cannot contain instance data but can include static methods with implementations.

2. **Multiple Inheritance**: Since C# does not support multiple inheritance of classes, interfaces allow a class to include behavior from multiple sources. Structs, which cannot inherit from other structs or classes, can simulate inheritance through interfaces.

3. **Defining an Interface**: An interface is defined using the `interface` keyword and follows a specific naming convention, typically starting with a capital `I`.

4. **Implementing Interfaces**: Any class or struct implementing an interface must provide definitions for all methods specified by the interface. For example, implementing `IEquatable<T>` requires an `Equals` method with a matching signature.

5. **Interface Members**: ==Interfaces can contain instance methods, properties, events, and indexers.== Starting with C# 8.0, interfaces can define default implementations for members.

6. **Access Modifiers**: Interface members are public by default, but can explicitly specify different access modifiers. A private member in an interface must have a default implementation.

7. **Implementation Requirements**: When implementing an interface, the corresponding class or struct members must be public, non-static, and match the interface member's name and signature.

8. **Static Members in Interfaces**: If an interface declares static members, implementing types can also declare static members with the same signature, but they are distinct and do not override the interface's static members.

9. **Inheritance and Interface Members**: If a base class implements an interface, derived classes inherit that implementation. However, a class can only implement an interface once and must declare it in its class definition.

10. **Interface Inheritance**: Interfaces can inherit from other interfaces, and a class implementing a derived interface must implement all members, including those from base interfaces.

11. **Virtual Interface Members**: Base classes can implement interface members as virtual, allowing derived classes to override and change the behavior.

12. **Interfaces Summary**: Interfaces are like abstract base classes with only abstract members (pre-C# 8.0), cannot be instantiated directly, and a class or struct can implement multiple interfaces.


Give examples to show how Csharp Interfaces contain instance methods, properties, events, and indexers.

## C# Interfaces: Instance Methods, Properties, Events, and Indexers

C# interfaces define contracts for classes to implement. They can contain:

* **Instance Methods:** These are methods declared in the interface but without implementation. Implementing classes must provide concrete implementations for these methods.

```csharp
public interface IShape
{
    double CalculateArea(); // Instance method
    double CalculatePerimeter(); // Instance method
}

public class Circle : IShape
{
    public double CalculateArea() 
    { 
        // Implementation for Circle's area calculation 
    }

    public double CalculatePerimeter() 
    { 
        // Implementation for Circle's perimeter calculation 
    }
}

```

* **Properties:** Similar to instance methods, properties declared in an interface define get and set accessors. Implementing classes must provide concrete implementations for these accessors.

```csharp
public interface IProduct
{
    string Name { get; set; } // Property with get and set accessors
    decimal Price { get; } // Property with only a get accessor
}

public class Book : IProduct
{
    public string Name { get; set; } 

    public decimal Price { get; } 
}
```

* **Events:** Interfaces can declare events, allowing classes to subscribe to notifications about specific occurrences. Implementing classes must define the event handler method.

```csharp
public interface INotifier
{
    event EventHandler SomethingHappened; // Event declaration
}

public class MyNotifier : INotifier
{
    public event EventHandler SomethingHappened;

    public void TriggerEvent() 
    { 
        SomethingHappened?.Invoke(this, EventArgs.Empty); // Raise the event
    }
}

```

* **Indexers:** Interfaces can define indexers, providing a way to access elements within an object using an index. Implementing classes must provide the logic for retrieving or setting values based on the index.

```csharp
public interface IStringCollection
{
    string this[int index] { get; set; } // Indexed property
}

public class MyStringCollection : IStringCollection
{
    private string[] strings = new string[10];

    public string this[int index] 
    { 
        get { return strings[index]; } 
        set { strings[index] = value; } 
    }
}

```



These examples demonstrate how C# interfaces can define contracts for classes, specifying the methods, properties, events, and indexers they must implement. This promotes code reusability, maintainability, and polymorphism.
