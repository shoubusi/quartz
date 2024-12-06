---
tags:
  - review
  - library
sr-due: 2024-08-28
sr-interval: 1
sr-ease: 230
---
# Polly

https://github.com/App-vNext/Polly
https://learn.microsoft.com/en-us/dotnet/core/resilience/

## Microsoft.Extensions.Resilience

The `Microsoft.Extensions.Resilience` package and the `Polly` package are closely related in the context of building resilient .NET applications. Here's an overview of their relationship:

1. **Polly**:
   - Polly is a comprehensive .NET library that provides resilience and transient-fault-handling capabilities.
   - It offers a variety of policies such as Retry, Circuit Breaker, Timeout, Bulkhead Isolation, and Fallback.
   - Polly is widely used to handle transient faults and ensure the stability of applications by defining how to handle failures.

2. **Microsoft.Extensions.Resilience**:
   - The `Microsoft.Extensions.Resilience` package is part of the Microsoft.Extensions suite, which provides integration with Polly.
   - It leverages Polly to offer resilience strategies within the Microsoft.Extensions ecosystem, making it easier to configure and use Polly policies with dependency injection and other .NET Core features.
   - This package simplifies the integration of Polly policies into .NET applications by providing a more seamless and idiomatic way to configure resilience strategies.

### Key Points of Integration

- **Configuration**:
  - `Microsoft.Extensions.Resilience` allows you to configure Polly policies using the standard .NET configuration system.
  - Example:
    ```csharp
    services.AddHttpClient("MyClient")
            .AddPolicyHandler(GetRetryPolicy());
    
    IAsyncPolicy<HttpResponseMessage> GetRetryPolicy()
    {
        return HttpPolicyExtensions
               .HandleTransientHttpError()
               .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
    }
    ```

- **Dependency Injection**:
  - The package integrates Polly policies with the .NET Core dependency injection (DI) system.
  - Example:
    ```csharp
    services.AddHttpClient("MyClient")
            .AddPolicyHandlerFromRegistry("MyRetryPolicy");
    
    services.AddPolicyRegistry()
            .Add("MyRetryPolicy", HttpPolicyExtensions
                .HandleTransientHttpError()
                .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt))));
    ```

- **HttpClientFactory**:
  - `Microsoft.Extensions.Resilience` works seamlessly with `HttpClientFactory`, allowing you to apply Polly policies to HTTP clients.
  - Example:
    ```csharp
    services.AddHttpClient("MyClient")
            .AddPolicyHandler(GetRetryPolicy())
            .AddPolicyHandler(GetCircuitBreakerPolicy());
    
    IAsyncPolicy<HttpResponseMessage> GetCircuitBreakerPolicy()
    {
        return HttpPolicyExtensions
               .HandleTransientHttpError()
               .CircuitBreakerAsync(5, TimeSpan.FromSeconds(30));
    }
    ```

### Summary

- **Polly** provides the core resilience and fault-handling capabilities.
- **Microsoft.Extensions.Resilience** builds on top of Polly, integrating it with the .NET Core ecosystem, making it easier to configure and use Polly policies with dependency injection, configuration, and `HttpClientFactory`.

By using `Microsoft.Extensions.Resilience`, developers can leverage the powerful features of Polly while benefiting from the seamless integration and configuration capabilities provided by the Microsoft.Extensions framework.

## Feature

Explain the key features of the Polly package in .NET, offering some examples

The Polly package in.NET is a powerful resilience and transient fault handling library. Here are its key features:

**1. Retry Policy**:
   - Allows you to automatically retry an operation that may have failed due to transient errors. For example, if a database connection fails momentarily due to a network glitch, Polly can retry the operation a specified number of times.
   - Example:
     ```csharp
     var policy = Policy.Handle<SqlException>()
                    .Retry(3);
     policy.Execute(() => { /* database operation */ });
     ```

**2. Circuit Breaker Pattern**:
   - Prevents a system from continuously attempting to execute a failing operation, which could lead to cascading failures. Once a certain number of failures occur within a specified time period, the circuit breaker trips and further attempts are blocked for a while.
   - Example:
     ```csharp
     var breakerPolicy = Policy.Handle<Exception>()
                             .CircuitBreaker(2, TimeSpan.FromSeconds(10));
     breakerPolicy.Execute(() => { /* some operation */ });
     ```

**3. Timeout**:
   - Ensures that an operation does not run indefinitely. If an operation takes longer than the specified timeout period, it is aborted.
   - Example:
     ```csharp
     var timeoutPolicy = Policy.Timeout(TimeSpan.FromSeconds(5));
     timeoutPolicy.Execute(() => { /* operation with potential to run long */ });
     ```

**4. Fallback**:
   - Defines an alternative action to take when an operation fails. This can be useful for providing a default response or gracefully degrading the functionality.
   - Example:
     ```csharp
     var fallbackPolicy = Policy.Handle<Exception>()
                              .Fallback(() => { return "Fallback value"; });
     var result = fallbackPolicy.Execute(() => { /* operation that may fail */ });
     ```

In summary, Polly provides a flexible and comprehensive set of tools for handling transient faults and improving the resilience of.NET applications.