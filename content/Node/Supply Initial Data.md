---
date created: 2024-08-16
date modified: 2024-10-15
---

# Supply Initial Data

This lesson explains how to specify initial data in your application.

## Implement the Module Updater

Open the _MySolution.Module\DatabaseUpdate\Updater.cs_ and override the [ModuleUpdater.UpdateDatabaseAfterUpdateSchema](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.Updating.ModuleUpdater.UpdateDatabaseAfterUpdateSchema) method

XAF uses an [Object Space](https://docs.devexpress.com/eXpressAppFramework/113707/data-manipulation-and-business-logic/object-space) instance to manipulate persistent objects (see [Create, Read, Update and Delete Data](https://docs.devexpress.com/eXpressAppFramework/113711/data-manipulation-and-business-logic/create-read-update-and-delete-data)).

## Add the ModuleInfo Entity

The **ModuleInfo** entity mapped to the **ModuleInfo** table is used when the [XafApplication.CheckCompatibilityType](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.XafApplication.CheckCompatibilityType) property is set to **ModuleInfo**, to store the version information of the application modules. When a module assembly version is incremented, XAF compares the actual module versions with versions stored in the database. If versions differ, the database must be updated. To support the database update, an entity that implements the data model must have the **IModuleInfo** interface.[^2]

> [!note]
> If you use the [Solution Wizard](https://docs.devexpress.com/eXpressAppFramework/113624/installation-upgrade-version-history/visual-studio-integration/solution-wizard) to create an XAF solution, the **ModuleInfo** entity is added automatically by default.

```csharp
public class MySolutionEFCoreDbContext : DbContext {
    // ...
    public DbSet<DevExpress.ExpressApp.EFCore.Updating.ModuleInfo> ModuleInfo { get; set; }
}
```

## Run the application

XAF compares the application version with the database version. If the database version is older than the application version, then the application raises the [DatabaseVersionMismatch](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.XafApplication.DatabaseVersionMismatch) event. Each platform-specific project in your solution handles this event in the descendant of the [XafApplication](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.XafApplication) class: `BlazorApplication` class (ASP.NET Core Blazor) and `WinApplication` class (Windows Forms).[^1]

The application ==creates a database if the database does not exist==. After that, the application calls the [ModuleUpdater.UpdateDatabaseAfterUpdateSchema](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.Updating.ModuleUpdater.UpdateDatabaseAfterUpdateSchema) method. The method saves the required objects to the database.

For additional information on how database updates work, refer to the following topic: [Create and Update the Application's Database](Create%20and%20Update%20the%20Application's%20Database.md)

[^1]: https://docs.devexpress.com/eXpressAppFramework/402985/getting-started/in-depth-tutorial-blazor/define-data-model-and-set-initial-data/define-data-model-and-set-initial-data-with-ef-core/supply-initial-data-ef-core

[^2]: https://docs.devexpress.com/eXpressAppFramework/402992/business-model-design-orm/business-model-design-with-entity-framework-core/how-to-supply-initial-data-for-the-entity-framework-core-data-model
