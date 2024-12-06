---
customer: 
user: 
tags:
  - Issue
type: Issue
subject: 
archived: true
---
describe the struct naming convention in Csharp

C# follows several conventions when it comes to naming structs. While there aren't strict, enforced rules, adhering to these practices makes your code more readable and understandable for others (and yourself!).

**General Principles:**

* **PascalCase:** This is the most common convention for struct names in C#. Each word within the name starts with a capital letter, while no spaces are used.
    * Example: `CustomerData`, `Point3D`

* **Descriptive and Meaningful:** The name should clearly indicate what data the struct represents or its purpose. Avoid overly generic or ambiguous names.
    * Good: `OrderDetails`, `Vector2` 
    * Less good: `Info`, `ValueHolder`

**Additional Considerations:**

* **Data vs Functionality:** Structs are often used to represent simple data aggregates, but they can also contain methods. If your struct has significant functionality beyond basic data storage (e.g., complex calculations), you might consider using a class instead.
* **Immutability:**  Structs in C# are value types and are typically designed to be immutable (their values cannot change after creation). Reflect this immutability in the name if appropriate, perhaps by using suffixes like `Immutable` or prefixes like `ReadOnly`.

**Examples:**

```csharp
public struct CustomerData 
{
    public string FirstName;
    public string LastName;
    public int OrderId;
}

// Example with a method:

public struct Point3D 
{ 
   public double X { get; } 
   public double Y { get; } 
   public double Z { get; }

   public double DistanceToOrigin() 
   {
       return Math.Sqrt(X * X + Y * Y + Z * Z);
   } 
}

```


In C#, the naming convention for structs follows the general naming guidelines for types. Here's a concise description of the struct naming convention:

1. PascalCase: Use PascalCase for struct names.
   ```csharp
   struct Point
   ```

2. Noun or noun phrase: Name should be a noun or noun phrase.
   ```csharp
   struct CustomerRecord
   ```

3. No prefix: Don't use prefixes like "Struct" or "S".
   ```csharp
   // Good
   struct Vector3D
   // Avoid
   struct StructVector3D
   ```

4. Avoid single-letter names: Use descriptive names.
   ```csharp
   // Good
   struct Coordinate
   // Avoid
   struct C
   ```

5. Consider adding "Readonly" for immutable structs (C# 7.2+).
   ```csharp
   readonly struct ImmutablePoint
   ```

6. Use singular nouns for structs representing a single item.
   ```csharp
   struct Rectangle
   ```

7. Avoid abbreviations unless they're widely recognized.
   ```csharp
   // Good
   struct HttpRequest
   // Avoid
   struct HtReq
   ```

8. Consider suffixing with the domain-specific type.
   ```csharp
   struct GeoCoordinate
   struct ColorRgb
   ```

Remember, these are guidelines. The most important aspect is maintaining consistency within your codebase and team conventions.

