---
date created: 2023-08-30
date modified: 2023-10-20
---
访问修饰符

doc page
- https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers
- https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers
- https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/

modifiers
- [public](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/public)：同一程序集中的任何其他代码或引用该程序集的其他程序集都可以访问该类型或成员。 某一类型的公共成员的可访问性水平由该类型本身的可访问性级别控制。
- [private](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/private)：只有同一 `class` 或 `struct` 中的代码可以访问该类型或成员。
- [protected](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/protected)：只有同一 `class` 或者从该 `class` 派生的 `class` 中的代码可以访问该类型或成员。
- [internal](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/internal)：同一程序集中的任何代码都可以访问该类型或成员，但其他程序集中的代码不可以。 换句话说，`internal` 类型或成员可以从属于同一编译的代码中访问。
- [protected internal](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/protected-internal)：该类型或成员可由对其进行声明的程序集或另一程序集中的派生 `class` 中的任何代码访问。
- [private protected](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/private-protected)：该类型或成员可以通过从 `class` 派生的类型访问，这些类型在其包含程序集中进行声明。

The following seven accessibility levels can be specified using the access modifiers:

- [`public`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/public): Access isn't restricted.
- [`protected`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/protected): Access is limited to the containing class or types derived from the containing class.
- [`internal`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/internal): Access is limited to the current assembly.
- [`protected internal`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/protected-internal): Access is limited to the current assembly or types derived from the containing class.
- [`private`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/private): Access is limited to the containing type.
- [`private protected`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/private-protected): Access is limited to the containing class or types derived from the containing class within the current assembly.
- [`file`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/file): The declared type is only visible in the current source file. File scoped types are generally used for source generators.

This section also introduces the following concepts:

- [Accessibility Levels](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/accessibility-levels): Using the four access modifiers to declare six levels of accessibility.
- [Accessibility Domain](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/accessibility-domain): Specifies where, in the program sections, a member can be referenced.
- [Restrictions on Using Accessibility Levels](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/restrictions-on-using-accessibility-levels): A summary of the restrictions on using declared accessibility levels.

![](../../attachment/Pasted%20image%2020221220151819.png)

[sealed](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/sealed)
When applied to a class, the `sealed` modifier prevents other classes from inheriting from it.

[virtual](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/virtual)
The `virtual` keyword is used to modify a method, property, indexer, or event declaration and allow for it to be overridden in a derived class.

When a virtual method is invoked, the run-time type of the object is checked for an overriding member. ==The overriding member in the most derived class is called==, which might be the original member, if no derived class has overridden the member.

[static](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static)
Use the `static` modifier to declare a static member, which belongs to the type itself rather than to a specific object.

[abstract](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract)
The `abstract` modifier indicates that the thing being modified has a missing or incomplete implementation. The abstract modifier can be used with classes, methods, properties, indexers, and events. Use the `abstract` modifier in a class declaration to indicate that a class is intended only to be a base class of other classes, not instantiated on its own. Members marked as abstract must be implemented by non-abstract classes that derive from the abstract class.

> [!info] what is the difference between Csharp modifier virtual and abstract
> 
> In C#, the  `virtual`  and  `abstract`  modifiers are used to define methods that can be overridden in derived classes. 
> 
> The main difference between  `virtual`  and  `abstract`  is that a  `virtual`  method ==has an implementation in the base class==, but ==can be overridden in derived classes==, whereas an  `abstract`  method ==has no implementation in the base class== and ==must be implemented in any non-abstract derived class==.
> 
> Here are some key differences between  `virtual`  and  `abstract`  methods in C#:
> 
> - `virtual`  methods can be implemented in the base class, whereas  `abstract`  methods must be implemented in derived classes.
> - `virtual`  methods can be overridden in derived classes using the  `override`  keyword, whereas  `abstract`  methods must be implemented using the  `override`  keyword.
> - `virtual`  methods can have a default implementation, but  `abstract`  methods cannot.
> - `virtual`  methods can be called directly on an instance of the base class, whereas  `abstract`  methods cannot be called directly on any instance.
> 
> In summary,  `virtual`  and  `abstract`  modifiers are used to define methods that can be overridden in derived classes, but  `virtual`  methods have an implementation in the base class, whereas  `abstract`  methods do not.
