---
date created: 2024-10-15
date modified: 2024-10-15
---
# Database Migrations for XAF

## Setup Migrations

- Delete the existing database (if there is one) before you proceed, because Entity Framework Core does not take the existing database schema into consideration when it generates the first migration.
- Add the Microsoft.EntityFrameworkCore.Tools NuGet package to the MySolution.Module project. Build the solution.
	- The package's version must correspond to the version of EF Core supported in XAF.
- In the **MySolution.Module** project, go to the _BusinessObjects_ folder and open the _MySolutionDbContext.cs_ file. Edit the declaration of the `MySolutionDesignTimeDbContextFactory` class.
	- If you develop a non-XAF application that needs to reuse your XAF application's DbContext, make sure to add the change-tracking proxies extension in the DbContext creation code. [^1]
	- In the above code sample, the `optionsBuilder.UseChangeTrackingProxies` method enables the change-tracking proxies extension so that the application's UI correctly reflects changes in data model.[^2]

```csharp
namespace MySolution.Module.BusinessObjects;
//...
public class MySolutionDesignTimeDbContextFactory : IDesignTimeDbContextFactory<MySolutionEFCoreDbContext> {
   public MySolutionEFCoreDbContext CreateDbContext(string[] args) {
      // Throw new InvalidOperationException ("Make sure that the database connection string and connection provider are correct. After that, uncomment the code below and remove this exception.")
      var optionsBuilder = new DbContextOptionsBuilder<MySolutionEFCoreDbContext>();
      optionsBuilder.UseSqlServer("Integrated Security=SSPI;Pooling=false;Data Source=(localdb)\\mssqllocaldb;Initial Catalog=MySolution");
      //Automatically implements the INotifyPropertyChanged interface in the business objects
      optionsBuilder.UseChangeTrackingProxies();
      optionsBuilder.UseObjectSpaceLinkProxies();
      return new MySolutionEFCoreDbContext(optionsBuilder.Options);
   }
}
```

## add-migration and update-database

```
add-migration MyInitialMigrationName -StartupProject "MySolution.Module" -Project "MySolution.Module"

update-database -StartupProject "MySolution.Module" -Project "MySolution.Module"
```

```
add-migration AddEntityProjectAndItem -StartupProject "PE.Module" -Project "PE.Module" -Context "PEEFCoreDbContext"

update-database -StartupProject "PE.Module" -Project "PE.Module" -Context "PEEFCoreDbContext"
```

> [!info]
> - The StartupProject here is the Module project, not the Win project.
> - The connection string in DesignTimeDbContextFactory will be used.
> - Add the Microsoft.EntityFrameworkCore.Tools NuGet package to the Module project, not the Win project.

- [Set the correct startup project and default project](Node/EntityFrameworkCore%20Migration.md#Set%20the%20correct%20startup%20project%20and%20default%20project)
- [Parameters for the Add-Migration command](Parameters%20for%20the%20Add-Migration%20command.md)

[^1]: https://docs.devexpress.com/eXpressAppFramework/404292/business-model-design-orm/business-model-design-with-entity-framework-core/performance/change-tracking-performance-considerations#use-a-dbcontext-outside-of-an-xaf-application
[^2]: [DbContext-UseChangeTrackingProxies](DbContext-UseChangeTrackingProxies.md)