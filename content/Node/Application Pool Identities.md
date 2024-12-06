---
date created: 2023-10-07
date modified: 2023-10-07
---
# Application Pool Identities

https://learn.microsoft.com/en-us/iis/manage/configuring-security/application-pool-identities

> Worker processes in IIS 6.0 and in IIS 7 run as Network Service by default. Network Service is a [[built-in Windows identity]]. It doesn't require a password and has only user privileges; that is, it is relatively low-privileged.

> isolate IIS worker processes from other Windows system services and run IIS worker processes under unique identities

> a feature called "virtual accounts" that allows IIS to create a unique identity for each of its application pools.

> For every application pool you create, the Identity property of the new application pool is set to ApplicationPoolIdentity by default.

> For example, if you create an application pool with the name "MyNewAppPool," a security identifier with the name "MyNewAppPool" is created in the Windows Security system.

> the identity is not a real user account; it will not show up as a user in the Windows User Management Console.

> The good news is that application pool identities also use the machine account to access network resources. No changes are required.





