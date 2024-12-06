---
date created: 2023-05-28
date modified: 2024-11-27
tags:
  - review
  - ABP
  - knowledge
sr-due: 2025-03-25
sr-interval: 369
sr-ease: 290
archived: false
---

# Connection Strings

```
Data Source=localhost;Initial Catalog=EmployeeManager;Trusted_Connection=True;TrustServerCertificate=true
Data Source=localhost;Initial Catalog=EmployeeManagerEasyTest;Trusted_Connection=True;TrustServerCertificate=true

```

## Integrated Security

Let me explain the `Integrated Security=SSPI` setting in SQL Server connection strings:

`Integrated Security=SSPI` (also written as `Integrated Security=True`) means that Windows Authentication (Windows credentials) will be used to connect to the SQL Server instead of SQL Server authentication.

When you use:
- `Integrated Security=SSPI`: The current Windows user's credentials are automatically used
- SQL Server authentication: You explicitly provide User ID and Password in the connection string

These two authentication methods are mutually exclusive - you cannot use both at the same time. If you include both:
- `Integrated Security=SSPI` will take precedence
- User ID and Password will be ignored

Example connection strings:

```
# Windows Authentication

Server=myserver;Database=mydatabase;Integrated Security=SSPI;

# SQL Server Authentication

Server=myserver;Database=mydatabase;User ID=myuser;Password=mypassword;
```

Best practice:
- Use Windows Authentication (Integrated Security) when possible as it's generally more secure
- Use SQL Server authentication when Windows Authentication isn't available (like in some cloud scenarios) or when specifically required by your application architecture

## TrustServerCertificate

证书链是由不受信任的颁发机构颁发的
`TrustServerCertificate=True;`

## Trusted_Connection

`Trusted_Connection=True;`

## Multiple Active Result Sets

For XAF, make sure that your connection strings include the following setting: `MultipleActiveResultSets=True;`.[^1]

## ApplicationIntent

`ApplicationIntent=ReadOnly`

1. **Meaning and Purpose**
    - The `ApplicationIntent = ReadOnly` in a connection string is used to indicate the intention of the application's connection to a SQL Server database. It tells the SQL Server that the application connecting to it will only perform read - only operations.
    - This is a valuable setting in scenarios such as a reporting application. For example, if you have a web - based reporting tool that queries a database to generate reports, setting `ApplicationIntent = ReadOnly` ensures that the application cannot accidentally or maliciously modify the data in the database.
2. **How it Affects the Database**
    - When this setting is used, the SQL Server can optimize the connection and the resources allocated to it. The database engine may route the connection to a read - only replica in a high - availability or disaster - recovery configuration. For example, in an Always On Availability Group setup in SQL Server, read - only replicas can handle read - only workloads, offloading the primary replica (which handles write operations) and improving overall performance.
    - It also helps in maintaining data integrity. Since the connection is marked as read - only, any attempt to execute write operations such as INSERT, UPDATE, or DELETE statements through this connection will result in an error. This provides an additional layer of protection against accidental data modification.
3. **Use Cases**
    - **Reporting and Analytics**: Many business intelligence and reporting tools use this setting. For instance, a data analytics dashboard that queries a large database to display charts and graphs. By using a read - only connection, the dashboard can access and present data without any risk of changing the underlying data.
    - **Data Warehousing**: In a data warehouse environment, where data is typically loaded in batches and then used for querying and analysis, read - only connections are common. Applications that access the data warehouse for generating reports or performing data mining operations can use `ApplicationIntent = ReadOnly` to ensure the integrity of the stored data.

## Pooling

`Pooling=false`

1. **What is Connection Pooling?**
    - Connection pooling is a mechanism used by database access libraries to manage and reuse database connections. When connection pooling is enabled (the default in many cases), the system creates a pool of database connections. When an application requests a connection to the database, instead of creating a brand - new connection every time, it retrieves an existing connection from the pool. After the application is done using the connection, instead of closing it completely, the connection is returned to the pool so that it can be reused by other parts of the application. This can significantly improve the performance of the application, especially in scenarios where there are frequent requests to connect to the database.
2. **Meaning of Pooling = false**
    - When you set `Pooling = false` in a connection string, you are disabling the connection pooling feature. This means that every time your application requests a connection to the database, a new, dedicated connection will be created. And when the application is done using the connection, the connection will be closed and disposed of, not returned to a pool for reuse.
3. **Reasons for Disabling Pooling**
    - **Resource Management**: In some cases, you might want to have precise control over the number of connections to the database. For example, if your application has a very limited and well - defined set of database access patterns and you want to ensure that there are no lingering connections or unexpected behavior due to connection reuse, you might choose to disable pooling.
    - **Connection - Specific Behavior**: If the connection needs to have some unique settings or behaviors that are not compatible with the connection pool (such as a special initialization routine that should only be run once per connection and not when a connection is reused from the pool), disabling pooling can be a better option.
    - **Testing and Debugging**: During the development and testing phase, disabling pooling can make it easier to track and debug connection - related issues. Since each connection is a new and separate entity, it can be simpler to isolate problems such as connection leaks or incorrect configuration settings for individual connections.
## Reference

https://www.connectionstrings.com/

https://docs.abp.io/en/abp/latest/Connection-Strings

[^1]: https://docs.devexpress.com/eXpressAppFramework/404348/business-model-design-orm/business-model-design-with-entity-framework-core/importance-of-multiple-active-result-sets
