---
date created: 2023-08-16
date modified: 2023-08-16
source: bito
---

Inversion of Control

Inversion of Control (IoC) is a ==software design principle== that promotes loose coupling and separation of concerns in a system. It is closely related to the [[../../Node/Dependency Injection]] (DI) pattern.

In IoC, the control flow and responsibility of ==managing dependencies== are inverted or handed over to ==an external container or framework==. Instead of a component or class being responsible for creating and managing its dependencies, the dependencies are provided or injected into the component from an external source.

IoC helps to decouple different components or classes, making them more modular and reusable. It allows for better separation of concerns and promotes the Single Responsibility Principle (SRP) by ensuring that each component focuses on its specific task.

IoC containers or frameworks, such as Unity, Autofac, Ninject, or Microsoft.Extensions.DependencyInjection in C#, are commonly used to implement IoC. These containers handle the creation, resolution, and lifetime management of dependencies, allowing components to be loosely coupled and easily replaced or extended.

Overall, Inversion of Control is a design principle that promotes loose coupling and separation of concerns by inverting the responsibility of managing dependencies to an external container or framework.
