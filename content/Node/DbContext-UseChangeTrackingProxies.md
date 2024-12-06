---
customer:
user:
tags:
  - Issue
type: Issue
subject:
archived: false
---
explain the meaning of `options.UseChangeTrackingProxies()` in DbContext settings

The `options.UseChangeTrackingProxies()` method is an important configuration option when using Entity Framework Core with XAF. Here's an explanation of its purpose and significance:

1. Change Tracking:
   Entity Framework Core needs to track changes made to entities so it can generate appropriate database update commands when you save changes. 

2. Proxy Creation:
   By calling `UseChangeTrackingProxies()`, you're enabling EF Core to create dynamic proxy classes for your entity types at runtime. These proxies wrap your entity classes and add change tracking behavior.

3. Virtual Properties:
   For this to work effectively, your entity properties should be declared as virtual. This allows the proxy to override them and inject the change tracking logic.

4. Performance Considerations:
   While this adds some overhead, it's generally more efficient than other change tracking strategies for most scenarios.

5. XAF Integration:
   XAF relies on property change notifications to keep the UI in sync with the data model. The change tracking proxies automatically implement `INotifyPropertyChanged` and `INotifyPropertyChanging` interfaces, which XAF uses for this purpose.

6. Automatic Notifications:
   Without this option, you would need to manually implement property change notifications in all your entity classes, which can be tedious and error-prone.

7. Consistency:
   It ensures that all entities, including those from XAF's built-in modules, use the same change tracking mechanism.

In summary, `options.UseChangeTrackingProxies()` is a crucial configuration for XAF applications using Entity Framework Core. It simplifies your entity classes, improves change tracking performance, and ensures proper integration with XAF's UI update mechanisms.