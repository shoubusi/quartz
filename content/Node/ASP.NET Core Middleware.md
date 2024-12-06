---
tags: knowledge
archived: false
---

# ASP.NET Core Middleware

ASP.NET Core middleware is a fundamental concept in the ASP.NET Core framework, responsible for handling HTTP requests and responses. Middleware components are assembled into a pipeline to process requests and generate responses. Here are the key concepts of ASP.NET Core middleware:

## Key Concepts

### 1. **Middleware Pipeline**
   - The middleware pipeline is a sequence of middleware components that process HTTP requests and responses.
   - Each middleware component can perform operations before and after the next component in the pipeline is invoked.
   - The pipeline is configured in the `Startup.Configure` method.

### 2. **Middleware Components**
   - Middleware components are classes that handle HTTP requests and responses.
   - Each component has access to the `HttpContext` and can perform actions such as logging, authentication, routing, etc.
   - Middleware components are typically added to the pipeline using extension methods on `IApplicationBuilder`.

### 3. **Request Delegation**
   - Middleware components can either handle the request themselves or pass it to the next component in the pipeline.
   - This is achieved using the `next` delegate, which represents the next middleware in the pipeline.

### 4. **Creating Middleware**
   - Middleware can be created by implementing a class with an `Invoke` or `InvokeAsync` method.
   - Example:
 ```csharp
 public class CustomMiddleware
 {
	 private readonly RequestDelegate _next;

	 public CustomMiddleware(RequestDelegate next)
	 {
		 _next = next;
	 }

	 public async Task InvokeAsync(HttpContext context)
	 {
		 // Pre-processing logic
		 await context.Response.WriteAsync("Hello from Custom Middleware!");

		 // Call the next middleware in the pipeline
		 await _next(context);

		 // Post-processing logic
	 }
 }
 ```

### 5. **Using Middleware**
   - Middleware is added to the pipeline in the `Startup.Configure` method using the `UseMiddleware` extension method.
   - Example:
 ```csharp
 public class Startup
 {
	 public void Configure(IApplicationBuilder app, IHostingEnvironment env)
	 {
		 app.UseMiddleware<CustomMiddleware>();

		 app.Run(async (context) =>
		 {
			 await context.Response.WriteAsync("Hello from the terminal middleware!");
		 });
	 }
 }
 ```

### 6. **Built-in Middleware**
   - ASP.NET Core provides several built-in middleware components for common tasks such as:
     - **Static Files**: Serves static files (e.g., HTML, CSS, JavaScript).
       ```csharp
       app.UseStaticFiles();
       ```
     - **Routing**: Routes requests to the appropriate endpoint.
       ```csharp
       app.UseRouting();
       ```
     - **Authentication**: Handles authentication.
       ```csharp
       app.UseAuthentication();
       ```
     - **Authorization**: Handles authorization.
       ```csharp
       app.UseAuthorization();
       ```
     - **Exception Handling**: Handles exceptions and displays error pages.
       ```csharp
       app.UseExceptionHandler("/Home/Error");
       ```

### 7. **Order of Middleware**
   - The order in which middleware components are added to the pipeline is crucial.
   - Middleware components are executed in the order they are added, and the response flows back through the pipeline in reverse order.
   - Example:
     ```csharp
     public void Configure(IApplicationBuilder app, IHostingEnvironment env)
     {
         app.UseMiddleware<FirstMiddleware>();
         app.UseMiddleware<SecondMiddleware>();
         app.UseMiddleware<ThirdMiddleware>();
     }
     ```

### 8. **Terminal Middleware**
   - Terminal middleware is the last middleware in the pipeline and does not call the `next` delegate.
   - It handles the request and generates the response directly.
   - Example:
     ```csharp
     app.Run(async (context) =>
     {
         await context.Response.WriteAsync("Hello from the terminal middleware!");
     });
     ```

### Summary

- **Middleware Pipeline**: A sequence of middleware components that process HTTP requests and responses.
- **Middleware Components**: Classes that handle HTTP requests and responses, added to the pipeline using `IApplicationBuilder`.
- **Request Delegation**: Middleware can pass the request to the next component using the `next` delegate.
- **Creating Middleware**: Implement a class with an `Invoke` or `InvokeAsync` method.
- **Using Middleware**: Add middleware to the pipeline in the `Startup.Configure` method.
- **Built-in Middleware**: ASP.NET Core provides built-in middleware for common tasks.
- **Order of Middleware**: The order of middleware components in the pipeline is crucial.
- **Terminal Middleware**: The last middleware in the pipeline that handles the request directly.

Middleware is a powerful and flexible way to handle HTTP requests and responses in ASP.NET Core, allowing developers to build robust and modular web applications.