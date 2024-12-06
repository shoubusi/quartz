---
date created: 2022-12-29
date modified: 2023-03-07
---
# ISNULL

https://learn.microsoft.com/zh-cn/sql/t-sql/functions/isnull-transact-sql?view=sql-server-ver16

explain the usage of ISNULL function in T-SQL

The `ISNULL` function is a SQL Server (Transact-SQL) function used to handle NULL values by replacing them with an alternative value if necessary. This can be very useful when you want to provide meaningful results even when certain pieces of data are missing or null.

**Syntax:**

```sql
ISNULL(value1, value2)
```

- **value1:** The expression that may return a value.
- **value2:** (Optional) A second expression used if `value1` is NULL. If this argument is omitted and `value1` is NULL, the function returns NULL.

**Example Usage:**

Suppose you have a table named `Sales` with columns for `CustomerID`, `OrderDate`, and `Quantity`. You want to calculate total sales amount but need to handle missing or null order dates gracefully. Here's how you could use ISNULL:

```sql
SELECT CustomerID, OrderDate,
       Quantity * Price AS SalesAmount,
       ISNULL(OrderDate, '2023-01-01') AS SafeOrderDate  -- Defaulting to a specific date if OrderDate is null
FROM Sales;
```

In this example, the `ISNULL` function checks whether `OrderDate` is NULL. If it is (meaning no order date was provided), then '2023-01-01' will be used instead.

**Key Points to Remember:**

1. **Type Compatibility:** The types of both arguments must match, or the argument that doesn't fit will be converted to a compatible type.
   
2. **Precedence Over Other Functions:** `ISNULL` is evaluated before other arithmetic operations and aggregations when it's used in a SELECT clause.

3. **Handling Multiple NULLs:** If you need to handle multiple columns with potential NULL values, you can use nested ISNULL calls or CASE expressions for more complex logic:

   ```sql
   SELECT CustomerID,
          OrderDate,
          Quantity * Price AS SalesAmount,
          ISNULL(OrderDate, '2023-01-01') AS SafeOrderDate,
          ISNULL(Price, 0) AS SafePrice -- Assuming Price might also be null
   FROM Sales;
   ```

4. **Combining with COALESCE:** `COALESCE` is another function that can be used to handle NULL values by returning the first non-NULL argument:

   ```sql
   SELECT CustomerID,
          OrderDate,
          Quantity * COALESCE(Price, 0) AS SalesAmount -- Defaulting Price to 0 if null
   FROM Sales;
   ```

**Conclusion:** The `ISNULL` function is a useful tool in SQL when you need to handle NULL values gracefully. By replacing them with alternative data or default values, it helps ensure your queries return meaningful and usable results even when data might be missing from the database.