### How to display my entities in the Navigation System

To display your entities in the XAF Navigation System, you have a few options:

1. Use attributes on your entity classes:

   Add the `[DefaultClassOptions]` attribute to your entity class:

   ```csharp
   [DefaultClassOptions]
   public class MyEntity : BaseObject {
     // ...
   }
   ```

   This will automatically add a navigation item for the entity's ListView.

   Or use the more specific `[NavigationItem]` attribute:

   ```csharp
   [NavigationItem("MyGroup")]
   public class MyEntity : BaseObject {
     // ...
   }
   ```

   This adds the entity to a specific navigation group.

2. Configure in the Application Model:

   - Open the Model Editor
   - Navigate to the NavigationItems node
   - Add a new NavigationItem node 
   - Set its View property to the ListView for your entity (e.g. "MyEntity_ListView")

3. Add programmatically:

   In a Controller, you can add items to the navigation:

   ```csharp
   public class MyController : WindowController {
     protected override void OnActivated() {
       base.OnActivated();
       IModelNavigationItem navItem = Application.Model.NavigationItems.AddNode<IModelNavigationItem>();
       navItem.View = Application.FindListViewId(typeof(MyEntity));
     }
   }
   ```

4. For non-persistent objects:

   You need to populate the objects in the NonPersistentObjectSpace.ObjectsGetting event.

The key things are:

- Use attributes for simple cases
- Use the Model Editor for more control over structure
- Add programmatically for dynamic navigation
- Ensure non-persistent objects are populated

After adding navigation items, they will appear in the navigation control (e.g. accordion, tree, etc.) allowing users to open the corresponding Views.