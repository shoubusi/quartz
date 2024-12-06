---
date created: 2023-08-14
date modified: 2023-08-23
tags: WPF
---

# Data Binding

## Data binding basics 

In WPF, we use the Binding class to create our bindings. 
every binding will contain four constituent parts.

- The first is the ==binding source==; typically, this will be one of our View Models. 
- The second is the ==path to the property from the source object== that we would like to data bind to. 
- The third is the ==binding target==; this will typically be a UI control. 
- The fourth is the ==path to the property of the binding target== that we want to data bind to.

## Binding path syntax

the binding path is relative to the binding source 
that the binding source is typically set by the DataContext property, or by the path itself. 
In order to bind to the whole binding source, we can specify our binding like this:

- `{Binding Path=.}`
- `{Binding .} `
- `{Binding}`

We will omit the Path property declaration in the bindings in this book for brevity.

when binding directly to the property of a data bound object, we just use the property name:
`{Binding PropertyName}`

```xml
    <dxlc:LayoutControl Orientation="Vertical" VerticalAlignment="Top">
        <ListBox x:Name="itemsList" SelectedIndex="0">
            <sys:String>First</sys:String>
            <sys:String>Second</sys:String>
            <sys:String>Third</sys:String>
        </ListBox>
        <Button Command="{Binding ShowDetailCommand}" CommandParameter="{Binding SelectedItem, ElementName=itemsList}" Content="Show Detail"/>
    </dxlc:LayoutControl>
```

Other than setting the [DataContext](https://learn.microsoft.com/en-us/dotnet/api/system.windows.frameworkelement.datacontext) property on an element directly, inheriting the [DataContext](https://learn.microsoft.com/en-us/dotnet/api/system.windows.frameworkelement.datacontext) value from an ancestor (such as the button in the first example), and explicitly specifying the binding source by setting the [Binding.Source](https://learn.microsoft.com/en-us/dotnet/api/system.windows.data.binding.source) property on the binding (such as the button the last example), you can also use the [Binding.ElementName](https://learn.microsoft.com/en-us/dotnet/api/system.windows.data.binding.elementname#system-windows-data-binding-elementname) property or the [Binding.RelativeSource](https://learn.microsoft.com/en-us/dotnet/api/system.windows.data.binding.relativesource#system-windows-data-binding-relativesource) property to specify the binding source. The [ElementName](https://learn.microsoft.com/en-us/dotnet/api/system.windows.data.binding.elementname) property is useful when you're binding to other elements in your app, such as when you're using a slider to adjust the width of a button. The [RelativeSource](https://learn.microsoft.com/en-us/dotnet/api/system.windows.data.binding.relativesource) property is useful when the binding is specified in a [ControlTemplate](https://learn.microsoft.com/en-us/dotnet/api/system.windows.controls.controltemplate) or a [Style](https://learn.microsoft.com/en-us/dotnet/api/system.windows.style). For more information, see [Binding sources overview](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/data/binding-sources-overview?view=netdesktop-7.0).

## With DX

## Reference

- [Mastering Windows Presentation Foundation](../../Node/Mastering%20Windows%20Presentation%20Foundation.md)
- https://learn.microsoft.com/en-us/dotnet/desktop/wpf/data/?view=netdesktop-7.0

- [ ] UpdateSourceTrigger
