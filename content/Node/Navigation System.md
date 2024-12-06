
# Navigation System

## Key Concepts

Based on the documentation, here are the key concepts of the XAF Navigation System:

1. Navigation Structure:
   - Defined in the Application Model under the IModelRootNavigationItems node
   - Consists of IModelNavigationItem nodes, which can have child nodes
   - Reflects the relationship between different Views in the application

2. Navigation Control:
   - The UI element that displays the navigation structure to users
   - Allows users to switch between different Views
   - Can be customized in style and appearance

3. Navigation Items:
   - Correspond to Views or serve as grouping elements
   - If an item has the View property set, selecting it activates that View
   - If the View property is not set, the item acts as a group for other items

4. ShowNavigationItemController:
   - Populates the navigation Action Container with navigation Actions
   - Reads the navigation structure and control style settings from the Application Model
   - Customizes the navigation control accordingly
   - Synchronizes the selected item in the navigation control with the active View

5. Navigation Actions:
   - Matched by UI elements in the navigation control
   - Hosted in the navigation Action Container

6. Customization Options:
   - Add items to the navigation control
   - Rename and rearrange navigation items
   - Define different navigation control styles for different platforms (WinForms, ASP.NET Web Forms, ASP.NET Core Blazor)
   - Customize via code or through the Application Model

7. Platform-Specific Features:
   - WinForms: Multiple navigation styles (Accordion, Navigation Bar, Tree List, etc.)
   - ASP.NET Web Forms: Various navigation bar styles
   - ASP.NET Core Blazor: Accordion and Tree List styles

8. Images and Icons:
   - Can be shown for navigation items (controlled by IModelRootNavigationItems.ShowImages)

9. Startup Navigation:
   - Can set a specific View to show at application startup

10. Context Navigation:
    - Allows for dynamic navigation based on the current context or state of the application

The Navigation System in XAF provides a flexible way to organize and present the application's structure to users, with options for customization across different platforms and use cases.

## How-to

