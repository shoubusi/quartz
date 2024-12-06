---
tags:
  - review
date created: 2024-08-21
date modified: 2024-11-18
---

# Create and Update the Application's Database

<https://docs.devexpress.com/eXpressAppFramework/113185/business-model-design-orm/create-and-update-the-applications-database>

An application runs successfully when its version equals to the database version. So, each time an application starts, version compatibility is checked. During this process, the system is trying to access the database. When running an application for the first time, ==the database does not yet exist==. So, an exception is raised. ==This exception is not thrown==, but the [XafApplication.DatabaseVersionMismatch](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.XafApplication.DatabaseVersionMismatch) event is raised to give you an opportunity to create a database. ==So that you do not have to deal with proper database creation==, this event is handled in an XAF application template. See the XXXApplication.cs (XXXApplication.vb) file in your application projects.

For information on how to provide a connection string to your application's database, refer to the [Connect an XAF Application to a Database Provider](Node/Connect%20an%20XAF%20Application%20to%20a%20Database%20Provider.md) topic.

[automatic versioning for AssemblyVersion](Node/automatic%20versioning%20for%20AssemblyVersion.md)
