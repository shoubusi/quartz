---
tags: knowledge
archived: false
---
IServiceScope

IServiceScope is an interface in the .NET dependency injection (DI) system that represents a scope for resolving services. It is particularly useful for managing the lifetime of scoped services. Here are some common usages of IServiceScope:

1. **Creating a Scoped Lifetime**:
   - [IServiceScope](file:///d%3A/PG/ConsoleDI/ConsoleDI/Program.cs#27%2C9-27%2C9) is used to create a new scope, ensuring that scoped services are disposed of correctly when the scope is disposed.
   - Example:
     ```csharp
     using (var scope = serviceProvider.CreateScope())
     {
         var scopedService = scope.ServiceProvider.GetService<IMyScopedService>();
         // Use the scoped service
     } // scopedService is disposed here
     ```

2. **Using Scoped Services in Background Tasks**:
   - When running background tasks or hosted services, `IServiceScope` ensures that scoped services are properly managed.
   - Example:
     ```csharp
     public class MyBackgroundService : BackgroundService
     {
         private readonly IServiceProvider _serviceProvider;

         public MyBackgroundService(IServiceProvider serviceProvider)
         {
             _serviceProvider = serviceProvider;
         }

         protected override async Task ExecuteAsync(CancellationToken stoppingToken)
         {
             while (!stoppingToken.IsCancellationRequested)
             {
                 using (var scope = _serviceProvider.CreateScope())
                 {
                     var scopedService = scope.ServiceProvider.GetRequiredService<IMyScopedService>();
                     // Use the scoped service
                 }
                 await Task.Delay(1000, stoppingToken);
             }
         }
     }
     ```

3. **Using Scoped Services in ASP.NET Core Middleware**:
   - Middleware components can create a scope to resolve and use scoped services.
   - Example:
     ```csharp
     public class MyMiddleware
     {
         private readonly RequestDelegate _next;

         public MyMiddleware(RequestDelegate next)
         {
             _next = next;
         }

         public async Task InvokeAsync(HttpContext context, IServiceProvider serviceProvider)
         {
             using (var scope = serviceProvider.CreateScope())
             {
                 var scopedService = scope.ServiceProvider.GetRequiredService<IMyScopedService>();
                 // Use the scoped service
                 await _next(context);
             }
         }
     }
     ```

4. **Using Scoped Services in Console Applications**:
   - In console applications, `IServiceScope` can be used to manage the lifetime of scoped services.
   - Example:
     ```csharp
     static void Main(string[] args)
     {
         var serviceProvider = new ServiceCollection()
             .AddScoped<IMyScopedService, MyScopedService>()
             .BuildServiceProvider();

         using (var scope = serviceProvider.CreateScope())
         {
             var scopedService = scope.ServiceProvider.GetRequiredService<IMyScopedService>();
             // Use the scoped service
         } // scopedService is disposed here
     }
     ```

5. **Unit Testing with Scoped Services**:
   - In unit tests, `IServiceScope` can be used to create a scope for testing scoped services.
   - Example:
     ```csharp
     [Fact]
     public void TestScopedService()
     {
         var serviceProvider = new ServiceCollection()
             .AddScoped<IMyScopedService, MyScopedService>()
             .BuildServiceProvider();

         using (var scope = serviceProvider.CreateScope())
         {
             var scopedService = scope.ServiceProvider.GetRequiredService<IMyScopedService>();
             // Test the scoped service
         } // scopedService is disposed here
     }
     ```

In summary, `IServiceScope` is essential for managing the lifetime of scoped services, ensuring they are properly disposed of when no longer needed. It is widely used in various application scenarios, including background tasks, middleware, console applications, and unit testing.