---
date created: 2024-03-18
date modified: 2024-03-21
tags: DesignPattern
---
# FactoryMethod

- [FactoryMethodUml](FactoryMethodUml.md)
- [FactoryMethodCanvas](../../Canvas/FactoryMethodCanvas.canvas)

## Difference

what is the difference between factory method and [[AbstractFactory]]

In object-oriented design, the Factory Method pattern and the Abstract Factory pattern are both creational patterns used to create objects. 

The Factory Method pattern defines an interface for creating an object but lets subclasses decide which class to instantiate. This pattern allows a class to defer instantiation to its subclasses.

On the other hand, the Abstract Factory pattern provides an interface to create families of related or dependent objects without specifying their concrete classes. It's used to create a set of related objects, but the actual classes of the objects are not known beforehand.

In summary, the main difference is that the Factory Method pattern creates ==a single object==, while the Abstract Factory pattern creates ==families of related objects==.
