---
date created: 2023-10-20
date modified: 2023-11-16
tags:
  - review
  - ABP
  - knowledge
sr-due: 2026-01-22
sr-interval: 519
sr-ease: 250
archived: false
---

# Worker services in .NET



Worker services in .NET are a type of long-running background service that can be used to perform tasks outside the context of a web request. They are part of the `Microsoft.Extensions.Hosting` namespace and are typically used for tasks such as processing messages from a queue, performing scheduled tasks, or other background processing.

Here are the key concepts of Worker services in .NET:

### 1. **IHostedService Interface**
   - The `IHostedService` interface defines methods for starting and stopping background services.
   - It includes two methods: `StartAsync(CancellationToken cancellationToken)` and `StopAsync(CancellationToken cancellationToken)`.

### 2. **BackgroundService Class**
   - `BackgroundService` is an abstract base class that implements `IHostedService` and provides a convenient way to create long-running services.
   - It includes an abstract method `ExecuteAsync(CancellationToken stoppingToken)` where the background processing logic is implemented.

### 3. **Worker Class**
   - A typical worker service inherits from `BackgroundService` and overrides the `ExecuteAsync` method to implement the background task.
   - Example:
     ```csharp
     public class Worker : BackgroundService
     {
         private readonly ILogger<Worker> _logger;

         public Worker(ILogger<Worker> logger)
         {
             _logger = logger;
         }

         protected override async Task ExecuteAsync(CancellationToken stoppingToken)
         {
             while (!stoppingToken.IsCancellationRequested)
             {
                 _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);
                 await Task.Delay(1000, stoppingToken);
             }
         }
     }
     ```

### 4. **HostBuilder**
   - The `HostBuilder` is used to configure and run the worker service.
   - It sets up dependency injection, configuration, logging, and other services.
   - Example:
     ```csharp
     public class Program
     {
         public static void Main(string[] args)
         {
             CreateHostBuilder(args).Build().Run();
         }

         public static IHostBuilder CreateHostBuilder(string[] args) =>
             Host.CreateDefaultBuilder(args)
                 .ConfigureServices((hostContext, services) =>
                 {
                     services.AddHostedService<Worker>();
                 });
     }
     ```

### 5. **Dependency Injection**
   - Worker services can use dependency injection to access other services.
   - Services are registered in the `ConfigureServices` method of the `HostBuilder`.
   - Example:
     ```csharp
     public static IHostBuilder CreateHostBuilder(string[] args) =>
         Host.CreateDefaultBuilder(args)
             .ConfigureServices((hostContext, services) =>
             {
                 services.AddHostedService<Worker>();
                 services.AddSingleton<IMyService, MyService>();
             });
     ```

### 6. **Configuration and Logging**
   - Worker services can use the configuration and logging systems provided by `Microsoft.Extensions.Hosting`.
   - Configuration settings can be loaded from various sources such as JSON files, environment variables, and command-line arguments.
   - Example:
     ```csharp
     public static IHostBuilder CreateHostBuilder(string[] args) =>
         Host.CreateDefaultBuilder(args)
             .ConfigureAppConfiguration((hostingContext, config) =>
             {
                 config.AddJsonFile("appsettings.json", optional: true, reloadOnChange: true);
                 config.AddEnvironmentVariables();
             })
             .ConfigureLogging(logging =>
             {
                 logging.ClearProviders();
                 logging.AddConsole();
             })
             .ConfigureServices((hostContext, services) =>
             {
                 services.AddHostedService<Worker>();
             });
     ```

### 7. **Graceful Shutdown**
   - Worker services support graceful shutdown, allowing them to complete ongoing work before stopping.
   - The `StopAsync` method can be overridden to implement custom shutdown logic.
   - Example:
     ```csharp
     public class Worker : BackgroundService
     {
         protected override async Task ExecuteAsync(CancellationToken stoppingToken)
         {
             // Background task logic
         }

         public override async Task StopAsync(CancellationToken cancellationToken)
         {
             // Custom shutdown logic
             await base.StopAsync(cancellationToken);
         }
     }
     ```

### Summary
Worker services in .NET provide a robust framework for building long-running background tasks. They leverage the `IHostedService` interface and `BackgroundService` class, integrate seamlessly with dependency injection, configuration, and logging, and support graceful shutdown. This makes them ideal for a wide range of background processing scenarios in .NET applications.


[Worker Services in .NET](https://learn.microsoft.com/en-us/dotnet/core/extensions/workers)
[.NET Generic Host](Generic%20Host.md)
