---
status: done
---

Anonymous-types
https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/anonymous-types

[select-clause](select-clause.md)

```csharp
var collection = (from row in dt.Select() select new { Name = row["Name"], Created_time = (DateTime)row["Created"] });
```

