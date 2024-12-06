---
status: done
subject:
source: bito
---

What is the difference between IEnumerable and ObservableCollection

The difference between IEnumerable and ObservableCollection lies in their purpose and behavior in the context of data binding and collection manipulation.

1. IEnumerable:
   - IEnumerable is an interface provided by the .NET framework that represents a forward-only cursor for iterating over a collection of items.
   - It is the ==most basic interface for collections== and provides read-only access to the data.
   - IEnumerable is suitable when you ==only need to iterate over the collection and don't require dynamic changes to the collection itself==.
   - It does not provide any notifications when the collection is modified.

2. ObservableCollection:
   - ObservableCollection is a generic collection class provided by the .NET framework in the System.Collections.ObjectModel namespace.
   - It implements the INotifyCollectionChanged interface, which means it provides notifications when the collection is modified (items added, removed, or replaced).
   - ObservableCollection is suitable when you need to bind a collection to a UI element (like a ListBox or DataGrid) and want the UI to automatically update when the collection changes.
   - It allows dynamic addition and removal of items from the collection at runtime.

In summary, IEnumerable is a simple interface for iterating over a collection, while ObservableCollection is a specialized collection class that provides notifications for collection changes, making it suitable for data binding scenarios where the UI needs to reflect changes in the collection.



