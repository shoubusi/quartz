# Connect an XAF Application to a Database Provider

- When an application runs for the first time, its database is created automatically. 
- During the following runs in a debug mode, the application connects to the same database and updates it as required. 
- When the application runs in a release mode, the database is not updated by default. 

For details, refer to the [Create and Update the Application's Database](Create%20and%20Update%20the%20Application's%20Database.md) topic. If you ever need to have your database recreated, just drop it from the database server or remove the file, and it will be recreated automatically. 

By default, an XAF solution is configured to use an instance of the Microsoft SQL Server Express LocalDB on the local system, accessed via the integrated security. 

A database will be created on that server under the name of the solution you created. 

However, XPO and EF Core, which serve as an Object-Relational Mapping layer, support over a dozen database management systems. So you can change the default connection. To do this, you need to specify the required connection setting, and reference the required database provider connector assembly. This topic describes several approaches that allow you to connect an XAF application to the required database provider. [^1]


## Specify the Connection String via the Application Projects' Configuration Files

When you need to access the connection string in a compiled application, specify it via the application projects' configuration files.

- App.config - a WinForms application project's configuration file.
- Web.config - an ASP.NET Web Forms application project's configuration file.
- appsettings.json - an ASP.NET Core Blazor application project's configuration file.


[^1]: https://docs.devexpress.com/eXpressAppFramework/113155/business-model-design-orm/connect-an-xaf-application-to-a-database-provider