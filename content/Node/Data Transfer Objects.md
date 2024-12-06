---
date created: 2023-07-31
date modified: 2024-12-04
source: bito
aliases: [DTO]
tags:
  - review
sr-due: 2026-01-09
sr-interval: 506
sr-ease: 286
archived: false
---

# DTO

[Data Transfer Objects](https://docs.abp.io/en/abp/latest/Data-Transfer-Objects)

[Data Transfer Objects Best Practices](../../Node/Data%20Transfer%20Objects%20Best%20Practices.md)

what is DTO

DTO stands for Data Transfer Object. It is a design pattern commonly used in software development to transfer data between different layers or components of an application. 

DTOs are used to encapsulate data and provide a standardized way of transferring data between different parts of a system. They are often used to transfer data between the application's business logic layer and the presentation layer, such as between a server and a client in a web application.

DTOs typically contain only the necessary data fields and do not have any business logic or behavior associated with them. They are simple containers for data, usually in the form of properties or fields, and are often used to transfer data in a serialized format, such as JSON or XML.

By using DTOs, developers can decouple the data representation from the underlying implementation details, making it easier to manage and maintain the application's data transfer processes.

Describe the guildline to write DTO.
Should I create DTO as a POCO, or use existing library to help.

[Guidelines for Writing DTOs](Node/Guidelines%20for%20Writing%20DTOs.md)
