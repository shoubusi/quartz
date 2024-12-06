### How to hide key properties of entities from the UI by applying `Browsable(false)`﻿ attributes to them

To hide key properties of entities from the UI in XAF, you can apply the `[Browsable(false)]` attribute to those properties. Here's how to do it:

1. Open your entity class file.

2. Import the System.ComponentModel namespace if it's not already imported:

```csharp
using System.ComponentModel;
```

3. Apply the `[Browsable(false)]` attribute to the key property:

```csharp
[DefaultClassOptions]
public class MyEntity : BaseObject
{
    [Browsable(false)]
    [DevExpress.ExpressApp.Data.Key]
    public int ID { get; set; }

    // Other properties...
}
```

Key points:

- The `[Browsable(false)]` attribute hides the property from the UI.
- The `[DevExpress.ExpressApp.Data.Key]` attribute marks the property as the key for the entity.
- Make sure to use the `Key` attribute from the `DevExpress.ExpressApp.Data` namespace, not from `System.ComponentModel.DataAnnotations` or `DevExpress.Xpo`.

4. If you're using XPO, the key property is usually already implemented in the base class. In this case, you can override it and apply the `[Browsable(false)]` attribute:

```csharp
[DefaultClassOptions]
public class MyXPOEntity : XPObject
{
    public MyXPOEntity(Session session) : base(session) { }

    [Browsable(false)]
    public override int Oid
    {
        get { return base.Oid; }
        set { base.Oid = value; }
    }

    // Other properties...
}
```

5. For non-persistent objects, you can use a similar approach:

```csharp
[DomainComponent]
public class NonPersistentObject
{
    [Browsable(false)]
    [DevExpress.ExpressApp.Data.Key]
    public int Oid { get; set; }

    // Other properties...
}
```

By applying the `[Browsable(false)]` attribute, you ensure that the key properties are hidden from the UI in List Views, Detail Views, and other places where object properties are displayed, while still maintaining their functionality as key properties for the entities.