---

type: reference
---

- [x] Span-T-Struct ✅ 2024-08-16

https://learn.microsoft.com/en-us/dotnet/api/system.span-1?view=net-7.0
https://learn.microsoft.com/zh-cn/archive/msdn-magazine/2018/january/csharp-all-about-span-exploring-a-new-net-mainstay
https://zhuanlan.zhihu.com/p/449769032

https://learn.microsoft.com/en-us/dotnet/standard/memory-and-spans/memory-t-usage-guidelines

[operators-stackalloc](operators-stackalloc.md)



what is the scenario to use `Span<T> Struct` in csharp

`Span<T>` is a powerful and versatile struct in C# that provides a safe way to work with contiguous regions of memory. Here are key scenarios and use cases for `Span<T>`:

1. Efficient Memory Access:
   - Allows working with arrays, strings, or unmanaged memory without copying data.

2. Slicing Arrays or Strings:
```csharp
int[] array = { 1, 2, 3, 4, 5 };
Span<int> slice = array.AsSpan(1, 3); // [2, 3, 4]
```


3. Avoiding Array Allocations:
   - Use with `stackalloc` for stack-based memory allocation:
```csharp
Span<byte> buffer = stackalloc byte[128];
```


4. String Manipulation:
   - Efficient substring operations without allocations:
```csharp
ReadOnlySpan<char> text = "Hello, World!".AsSpan();
ReadOnlySpan<char> hello = text.Slice(0, 5); // "Hello"
```


5. Interop with Unmanaged Code:
   - Safely work with unmanaged memory:
```csharp
unsafe {
    byte* ptr = stackalloc byte[10];
    Span<byte> span = new Span<byte>(ptr, 10);
}
```


6. High-Performance Parsing:
   - Efficient parsing of data without allocations:
```csharp
ReadOnlySpan<char> input = "12345";
if (int.TryParse(input, out int result))
{
    // Use result
}
```


7. Buffer Manipulation:
   - Efficient buffer operations without copying:
```csharp
Span<byte> buffer = new byte[1024];
FillBuffer(buffer);
ProcessBuffer(buffer.Slice(0, 512));
```


8. Reducing Memory Fragmentation:
   - Work with parts of larger arrays without creating new ones.

9. API Design:
   - Accept `Span<T>` or `ReadOnlySpan<T>` in methods for flexibility:
```csharp
void ProcessData(ReadOnlySpan<byte> data) { ... }
```


10. Working with Memory-Mapped Files:
    - Efficiently access and manipulate file contents.

11. Custom Memory Management:
    - Create custom memory pools or allocation strategies.

12. SIMD Operations:
    - Efficiently perform vectorized operations on data.

Key Benefits:
- Improved performance by reducing allocations
- Enhanced safety when working with memory
- Flexibility in handling different memory sources

Considerations:
- `Span<T>` is a ref struct and has some usage restrictions (can't be used as a field in a class)
- Only represents contiguous memory
- Limited to a single dimension

`Span<T>` is particularly useful in scenarios where performance is critical and you need to work with memory efficiently without sacrificing safety. It's a key feature for writing high-performance C# code, especially in systems programming, data processing, and low-latency applications.