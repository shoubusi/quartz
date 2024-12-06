---
tags:




date created: 2023-01-10
date modified: 2023-01-30
---

- [x] operators/stackalloc #todo ✅ 2024-08-16

https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/stackalloc
https://zhuanlan.zhihu.com/p/258886046


what is the scenario to use stackalloc in csharp

`stackalloc` in C# is used for allocating memory on the stack rather than the heap. It's a specialized feature that can provide performance benefits in specific scenarios. Here are the key points about using `stackalloc`:

1. Use Cases:
   - Short-lived, small arrays
   - Performance-critical code
   - Avoiding heap allocations and garbage collection overhead

2. Syntax:
```csharp
Span<int> numbers = stackalloc int[100];
```

3. Key Characteristics:
   - Only works with value types
   - Can only be used in unsafe context or with `Span<T>` / `ReadOnlySpan<T>`
   - Memory is automatically freed when the method exits

4. Advantages:
   - Faster allocation and deallocation
   - No garbage collection overhead
   - Can improve cache locality

5. Limitations:
   - Limited size (usually up to a few kilobytes)
   - Risk of stack overflow if overused
   - Cannot be used for large allocations

6. Best Practices:
   - Use for small, known-size allocations
   - Avoid in recursive methods
   - Be cautious with user-supplied sizes

7. Example Use Case:
```csharp
public unsafe void ProcessData(int size)
{
    if (size <= 128)
    {
        Span<byte> buffer = stackalloc byte[size];
        // Use buffer for processing
    }
    else
    {
        // Fall back to heap allocation for larger sizes
        byte[] buffer = new byte[size];
        // Use buffer for processing
    }
}
```

8. Considerations:
   - Only use when profiling shows a clear benefit
   - Modern GC is very efficient, so benefits may be minimal in many cases
   - More useful in constrained environments or high-performance scenarios

Remember, `stackalloc` is an advanced feature. In most cases, regular heap allocation (`new`) is sufficient and safer. Use `stackalloc` only when you have a clear performance need and understand the implications fully.