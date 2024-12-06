---
status: done
subject:
source: bito
---

xaml namespaces


what does "xmlns:local" in xaml namespaces mean?

In XAML, the "xmlns:local" declaration is used to define a namespace alias for the local project or assembly. 

The "xmlns" attribute stands for XML Namespace and is used to define a mapping between a namespace and a prefix. The prefix is then used to reference elements or types from that namespace within the XAML code.

When you see "xmlns:local" in XAML, it means that ==a namespace alias with the prefix "local" is being created==. This ==allows you to reference elements or types from the local project or assembly using the "local" prefix.==

For example, if you have a custom control defined in your local project with the namespace "MyApp.Controls", you can use the "xmlns:local" declaration to create an alias for it like this:

`xmlns:local="clr-namespace:MyApp.Controls"`

Then, you can reference the custom control using the "local" prefix in your XAML code, like this:

`<local:MyCustomControl />`

This helps to keep the XAML code concise and readable by providing a shorter prefix for referencing elements or types from the local project or assembly.