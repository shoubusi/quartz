---
status: done
subject:
source: bito
date created: 2023-08-16
date modified: 2023-11-16
tags:
  - review
  - ABP
  - knowledge
sr-due: 2026-04-29
sr-interval: 670
sr-ease: 270
archived: false
---

# Dependency Injection

## Description

https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection

https://martinfowler.com/articles/injection.html

Dependency Injection (DI) is ==a design pattern and a technique== used in software development to achieve loose coupling between components or classes. It is a form of [[Inversion of Control]] (IoC) where ==the responsibility of creating and managing dependencies is shifted from the class itself to an external entity==.

In DI, instead of a class ==creating its own dependencies directly==, the dependencies are provided or injected into the class ==from an external source==, typically through ==constructor parameters or property setters==. This allows for better testability, flexibility, and maintainability of the codebase.

By using DI, classes can be easily decoupled from their dependencies, making them more modular and reusable. It also simplifies unit testing, as dependencies can be easily mocked or replaced with test doubles.

There are various DI frameworks and containers available in different programming languages, such as Unity, [[Autofac]], Ninject, and Microsoft.Extensions.DependencyInjection in C#. These frameworks provide mechanisms for managing and resolving dependencies automatically based on configuration and conventions.

## Dependency Injection in ABP Document

https://docs.abp.io/en/abp/latest/Dependency-Injection

## Service lifetimes

https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection#service-lifetimes

In the context of dependency injection, "Singleton", "Transient", and "Scoped" are different lifetimes or scopes for managing the lifetime of objects.  
  
1. Singleton: A singleton instance is created only once and shared across the entire application. It means that every time you request an instance of a singleton, you will get the same instance. This can be useful for objects that are expensive to create or need to maintain state throughout the application.  
  
2. Transient: A transient instance is created each time it is requested. This means that every time you request an instance of a transient object, you will get a new instance. Transient objects are typically used for lightweight, stateless services or objects that don't need to be shared.  
  
3. Scoped: A scoped instance is created once per scope. The scope can be defined as a logical boundary, such as a web request or a unit of work. Within the same scope, multiple requests for the same object will return the same instance. However, different scopes will have different instances. Scoped objects are useful when you want to share an instance within a specific context or boundary.  
  
To summarize:  
- Singleton: One instance shared across the entire application.  
- Transient: A new instance created every time it is requested.  
- Scoped: One instance per scope, multiple scopes can have different instances.  
  
The choice of lifetime depends on the specific requirements of your application and the behavior you want for your dependencies.

## Service registration methods

https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection#service-registration-methods

| Method                                                                                                                                                                                                | Automatic  <br>object  <br>disposal | Multiple  <br>implementations | Pass args |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | ----------------------------- | --------- |
| `Add{LIFETIME}<{SERVICE}, {IMPLEMENTATION}>()`  <br>  <br>Example:  <br>  <br>`services.AddSingleton<IMyDep, MyDep>();`                                                                               | Yes                                 | Yes                           | No        |
| `Add{LIFETIME}<{SERVICE}>(sp => new {IMPLEMENTATION})`  <br>  <br>Examples:  <br>  <br>`services.AddSingleton<IMyDep>(sp => new MyDep());`  <br>`services.AddSingleton<IMyDep>(sp => new MyDep(99));` | Yes                                 | Yes                           | Yes       |
| `Add{LIFETIME}<{IMPLEMENTATION}>()`  <br>  <br>Example:  <br>  <br>`services.AddSingleton<MyDep>();`                                                                                                  | Yes                                 | No                            | No        |
| `AddSingleton<{SERVICE}>(new {IMPLEMENTATION})`  <br>  <br>Examples:  <br>  <br>`services.AddSingleton<IMyDep>(new MyDep());`  <br>`services.AddSingleton<IMyDep>(new MyDep(99));`                    | No                                  | Yes                           | Yes       |
| `AddSingleton(new {IMPLEMENTATION})`  <br>  <br>Examples:  <br>  <br>`services.AddSingleton(new MyDep());`  <br>`services.AddSingleton(new MyDep(99));`                                               | No                                  | No                            | Yes       |


## Reference

[[IServiceProvider]]


[[IServiceScope]]

root scope

RequestServices

BackgroundService

[Worker services in .NET](Worker%20services%20in%20.NET.md)

HostApplicationBuilder
https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostapplicationbuilder?view=dotnet-plat-ext-7.0

using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;


explain the relationship of following types in context of Microsoft.Extensions.DependencyInjection and Microsoft.Extensions.Hosting
Host
HostApplicationBuilder
IHost
IServiceProvider
IServiceScope


There are 4 project in the module startup template of ABP:
- Application.Tests
- Domain.Tests
- EntityFrameworkCore.Tests
- TestBase

in which project should I place the DataSeedContributor.cs?
in DataSeedContributor.cs, I need to use EfCoreRepository to set initial data, but EfCoreRepository can not be access in some project
