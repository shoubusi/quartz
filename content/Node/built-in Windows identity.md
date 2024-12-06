---
date created: 2023-10-07
date modified: 2023-10-07
---

https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831797(v=ws.11)?redirectedfrom=MSDN#to-configure-an-application-pool-identity

**Built-in account**

Select this option to use one of the predefined security accounts. Then select one of the following accounts:

- **LocalService** - The Local Service account is a member of the Users group and has the same user rights as the Network Service account, but the Local Service account is limited to the local computer. Use this account when the worker process in your application pool ==does not require access outside the Web server on which it runs==.
- **LocalSystem** - The Local System account has all user rights, and it is part of the Administrators group on the Web server. Whenever possible, ==avoid using the Local System account because it presents a more serious security risk for your Web server==.
- **NetworkService** - By default, the Network Service account is selected. It is a member of the Users group and has user rights that are required to run applications. ==It can interact throughout an Active Directory-based network by using the credentials of the computer account==. This account provides the most security against an attack that might try to take over the Web server.

**Custom account**

Select this option to configure a custom account. Then click the corresponding **Set** button to configure the user name and password for the account.

If you use a custom identity, ~~make sure~~ that the user account you specify is a member of the [[IIS_IUSRS group]] on the Web server so that the account has proper access to resources.
