---
tags: knowledge
archived: false
---
# null-conditional operator

https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-

in csharp syntax, what does a question mark(?) after a instance name mean

You're talking about the **null-conditional operator** in C#. 

Here's the breakdown:

**What it does:**

The null-conditional operator (`?.`) is a shorthand way to safely access members (properties, methods, etc.) of an object *only if* that object is not null. 

**Syntax:**

`object?.member`

* **`object`:**  The instance you're checking for null.
* **`?`:** The null-conditional operator itself.
* **`member`:** The property, method, or indexer you want to access.

**How it works:**

1. **Null Check:** The `?.` operator first checks if the `object` is null.
2. **Safe Access:** If the `object` is *not* null, it proceeds to access the `member`.
3. **No Exception:** If the `object` *is* null, the entire expression evaluates to `null`, preventing a `NullReferenceException`.

**Example:**

```csharp
public class Person
{
    public string Name { get; set; }
}

Person person = null;

// Using the null-conditional operator:
string name = person?.Name; // name will be null because person is null

// Without the null-conditional operator (would throw an exception):
string name2 = person.Name; // Throws NullReferenceException
```

**Benefits:**

* **Readability:** Makes your code more concise and easier to understand.
* **Safety:** Prevents `NullReferenceExceptions` by handling null values gracefully.
* **Modern C#:** A key feature of modern C# that promotes safer and more reliable code.
