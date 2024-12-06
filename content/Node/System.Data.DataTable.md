System.Data.DataTable

https://learn.microsoft.com/en-us/dotnet/api/system.data.datatable

```
var collection = (from row in dt.Select() select new { Name = row["Name"], Created_time = (DateTime)row["Created"] });
```
