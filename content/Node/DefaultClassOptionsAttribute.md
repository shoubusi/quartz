---
date created: 2024-08-19
date modified: 2024-08-19
---
# DefaultClassOptionsAttribute

Sets default options for a class.[^1]
## Concept

The following default options are set when you apply `DefaultClassOptionsAttribute` to a business class:

- The corresponding item is added to the navigation control's Default navigation item. This allows users to display a View with objects of this class.
- The corresponding item is added to the **New** Action's Items list. This allows users to create objects of this class when objects of another type are displayed in the View.
- The corresponding item is added to the **Data Type** drop-down list in the Report Wizard. This allows users to create reports for objects of this class. For more information about how you can create and view reports in an XAF application, refer to the following topics:
    - [Create and View Reports in an ASP.NET Core Blazor Application](https://docs.devexpress.com/eXpressAppFramework/402306/shape-export-print-data/reports/create-and-view-reports-in-a-blazor-application)
    - [Create and View Reports in a WinForms Application](https://docs.devexpress.com/eXpressAppFramework/113646/shape-export-print-data/reports/create-and-view-reports-in-a-winforms-application)
    - [Create and View Reports in an ASP.NET Web Forms Application](https://docs.devexpress.com/eXpressAppFramework/113648/shape-export-print-data/reports/create-and-view-reports-in-an-asp-net-application)
- The corresponding item is added to the type list in the Dashboards Data Source Wizard. This allows users to create [dashboards](https://docs.devexpress.com/eXpressAppFramework/117449/analytics/dashboards-module) for objects of this class. For more information about how you can create, view, and modify Dashboards, refer to the following topics:
    - [Create, View, and Modify Dashboards in an ASP.NET Core Blazor Application](https://docs.devexpress.com/eXpressAppFramework/403400/analytics/dashboards/create-view-and-modify-dashboards-in-a-blazor-application)
    - [Create, View and Modify Dashboards in a WinForms Application](https://docs.devexpress.com/eXpressAppFramework/117450/analytics/dashboards/create-view-and-modify-dashboards-in-a-winforms-application)
    - [Create, View and Modify Dashboards in an ASP.NET Web Forms Application](https://docs.devexpress.com/eXpressAppFramework/117451/analytics/dashboards/create-view-and-modify-dashboards-in-an-asp-net-application)

If you do not want to set all the options specified above at the same time, use the following attributes:

- [CreatableItemAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.CreatableItemAttribute)
- [NavigationItemAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.NavigationItemAttribute)
- [VisibleInReportsAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.VisibleInReportsAttribute)
- [VisibleInDashboardsAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.VisibleInDashboardsAttribute).

## How to
[How to display my entities in the Navigation System](How%20to%20display%20my%20entities%20in%20the%20Navigation%20System.md)


[^1]: https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.DefaultClassOptionsAttribute
