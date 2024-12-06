---
date created: 2023-10-19
date modified: 2023-10-19
tags:
  - ABP
  - knowledge
archived: false
sr-due: 2024-09-26
sr-interval: 28
sr-ease: 290
---
#review 
# ABP Application Startup

https://docs.abp.io/en/abp/latest/Application-Startup
https://abp.io/get-started

## ABP.IO Platform Packages

ABP templates are being distributed as NuGet and NPM packages. Here are all the official NuGet and NPM packages used by the ABP.IO Platform.

https://abp.io/packages

## AbpApplicationFactory

https://docs.abp.io/en/abp/latest/Application-Startup#abpapplicationfactory

## Example

`MyConsoleDemoModule` class

```csharp
using Volo.Abp.Emailing;
using Volo.Abp.Modularity;

namespace MyConsoleDemo
{
    [DependsOn(typeof(AbpEmailingModule))] // Added the module dependency
    public class MyConsoleDemoModule : AbpModule
    {
    }
}
```

`Program.cs`

```csharp
using Microsoft.Extensions.DependencyInjection;
using MyConsoleDemo;
using Volo.Abp;
using Volo.Abp.Emailing;

using var application = await AbpApplicationFactory.CreateAsync<MyConsoleDemoModule>();
await application.InitializeAsync();

// Sending emails using the IEmailSender service
var emailsender = application.ServiceProvider.GetRequiredService<IEmailSender>();
await emailsender.SendAsync(
    to: "info@acme.com",
    subject: "Hello World",
    body: "My message body..."
);

await application.ShutdownAsync();
```