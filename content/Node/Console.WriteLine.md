---
type: reference
---
Console.WriteLine

https://learn.microsoft.com/zh-cn/dotnet/api/system.console.writeline?view=net-6.0
https://stackoverflow.com/questions/38538473/in-c-what-does-using-a-dollar-sign-do-in-console-writeline
https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated

```csharp
Span<int> numbers = new int[] { 3, 14, 15, 92, 6 };
foreach (int number in numbers)
{
    Console.Write($"{number} ");
}
// Output:
// 3 14 15 92 6
```
