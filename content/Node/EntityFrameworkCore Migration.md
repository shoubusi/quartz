---
customer:
user:
tags:
  - Issue
type: Issue
subject:
archived: false
---
# EntityFrameworkCore Migration


## Set the correct startup project and default project

When using Entity Framework tools in the Package Manager Console (PMC) for operations like `Add-Migration`, it's important to set the correct startup project and default project. Here's a guide on how to choose:

1. Startup Project:
   - This should be set to your main application project (usually a Web API, MVC, or Console application).
   - It's the project that contains your `Program.cs` or `Startup.cs` file.
   - This project typically has the connection string configuration.

2. Default Project in PMC:
   - This should be set to the project that contains your `DbContext` and entity classes.
   - Often, this is a separate class library project for your data access layer.

In your case, based on the file structure you've shown earlier:

1. Startup Project: 
   Set this to `SimpleProjectManager.Win` (assuming this is your main application project).

2. Default Project in PMC:
   Set this to the project that contains your `DbContext`. This might be a project named something like `SimpleProjectManager.Module` or `SimpleProjectManager.Data`.

To set these:

1. For the Startup Project:
   - Right-click on the desired project in Solution Explorer.
   - Select "Set as Startup Project".

2. For the Default Project in PMC:
   - Open the Package Manager Console.
   - Use the dropdown at the top of the PMC to select the project containing your `DbContext`.

Then, you can run your `Add-Migration` command:

```
Add-Migration YourMigrationName
```

Replace `YourMigrationName` with a descriptive name for your migration.

If you're still having issues, you can explicitly specify the context and project in the command:

```
Add-Migration YourMigrationName -Context YourDbContextName -Project YourDataProjectName
```

Remember, the exact project names and structure may vary based on your solution setup. Always ensure you're working with the correct projects to avoid confusion and potential errors in your database schema management.