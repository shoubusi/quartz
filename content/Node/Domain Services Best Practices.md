---
date created: 2023-11-16
date modified: 2023-11-16
tags:
  - review
  - ABP
  - knowledge
sr-due: 2026-01-04
sr-interval: 501
sr-ease: 290
archived: false
---

# Domain Services Best Practices & Conventions

https://docs.abp.io/en/abp/latest/Best-Practices/Domain-Services 


the best practices of ABP framework tells me "Do not define methods in Domain Services with generic names"
please explain it

The best practice of not defining methods in Domain Services with generic names is aimed at improving the clarity and maintainability of your codebase in the context of the ABP (ASP.NET Boilerplate) framework. Here's why this practice is recommended:

1. **Clarity and Intent**: By avoiding generic method names in Domain Services, you make the purpose and intent of each method clearer. Using specific and descriptive method names helps developers understand what each method does without needing to dive deep into the implementation.

2. **Avoid Ambiguity**: Generic method names like  `Process` ,  `Handle` , or  `Execute`  can be ambiguous and may lead to confusion when multiple methods with similar names exist in different domain services. Using specific names that reflect the operation being performed reduces this ambiguity.

3. **Code Maintainability**: When you use specific method names, it becomes easier to navigate and maintain the codebase. Developers can quickly identify the functionality they need and make changes without worrying about unintended side effects due to generic method names.

4. **Readability**: Specific method names improve the readability of the code and make it easier for new developers joining the project to understand the domain logic without extensive documentation.

In summary, following the best practice of using descriptive and specific method names in Domain Services helps improve code clarity, maintainability, and readability within the ABP framework. It promotes good coding practices and enhances the overall quality of your application.