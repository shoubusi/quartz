---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-12-21
date modified: 2023-12-21
archived: false
sr-due: 2024-11-29
sr-interval: 79
sr-ease: 290
---

# Auto API Controllers 

https://docs.abp.io/en/abp/latest/API/Auto-API-Controllers

Once you create an [application service](https://abp.io/docs/latest/framework/architecture/domain-driven-design/application-services), you generally want to create an API controller to expose this service as an HTTP (REST) API endpoint. A typical API controller does nothing but redirects method calls to the application service and configures the REST API using attributes like HttpGet, HttpPost, Route... etc.

ABP can **automagically** configure your application services as API Controllers by convention. Most of time you don't care about its detailed configuration, but it's possible to fully customize it.