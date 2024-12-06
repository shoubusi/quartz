---
date created: 2024-06-28
date modified: 2024-06-28
tags: knowledge
archived: false
---
# null-coalescing operator

The null-coalescing operator `??` returns the value of its left-hand operand if it isn't `null`; otherwise, it evaluates the right-hand operand and returns its result. The `??` operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null. 

The null-coalescing assignment operator `??=` assigns the value of its right-hand operand to its left-hand operand only if the left-hand operand evaluates to `null`. The `??=` operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null.

https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator


null-coalescing operator

Let's break down the null-coalescing operator (??).

**The Problem It Solves**

Imagine you're working with data that might be missing or undefined.  In programming, this often manifests as `null`.  Directly accessing a property of a `null` object leads to errors. The null-coalescing operator provides a safe and elegant way to handle this situation.

**How It Works**

The null-coalescing operator (`??`) acts like a conditional statement in a compact form:

* **Syntax:** `expression1 ?? expression2`
* **Logic:** 
    * If `expression1` evaluates to a truthy value (anything other than `null`, `undefined`, `0`, `false`, `""`), the operator returns the result of `expression1`.
    * If `expression1` evaluates to a falsy value (including `null` and `undefined`), the operator returns the result of `expression2`.

**Example**

```javascript
const user = { name: "Alice" };
const name = user?.name ?? "Guest"; // name will be "Alice"

const otherUser = null;
const otherName = otherUser?.name ?? "Guest"; // otherName will be "Guest"
```

**Key Benefits**

* **Readability:** The `??` operator makes your code more concise and easier to understand compared to lengthy if-else statements.
* **Safety:** It prevents errors caused by accessing properties of `null` or `undefined` objects.
* **Flexibility:** You can use it with any expression, not just object properties.

**Beyond the Basics**

* **Chaining:** You can chain multiple null-coalescing operators together for more complex scenarios.
* **Shorthand Assignment:** Use `??=` for updating values in a safe way.
