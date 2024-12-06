---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2024-03-28
sr-due: 2026-02-15
sr-interval: 543
sr-ease: 286
archived: false
---

# Unit of Work

[Unit of Work](https://docs.abp.io/en/abp/latest/Unit-Of-Work) 


[wucai-2024-05-13-H8536MF](../WuCai/2024/05/wucai-2024-05-13-H8536MF.md)

We are using `_issueRepository.GetQueryableAsync` to obtain an `IQueryable<Issue>` object. Then, we are using the `FirstOrDefaultAsync` method to query an issue by its title. The database query is executed at this point, and you get an exception indicating that there is no active unit of work.

To make that test properly working, you should manually start a unit of work scope as shown in the following example:

```csharp
public abstract class IssueRepository_Tests<TStartupModule> : MyProjectDomainTestBase<TStartupModule>
    where TStartupModule : IAbpModule
{
    private readonly IRepository<Issue, Guid> _issueRepository;
    private readonly IUnitOfWorkManager _unitOfWorkManager;

    protected IssueRepository_Tests()
    {
        _issueRepository = GetRequiredService<IRepository<Issue, Guid>>();
        _unitOfWorkManager = GetRequiredService<IUnitOfWorkManager>();
    }

    public async Task Should_Query_By_Title()
    {
        using (var uow = _unitOfWorkManager.Begin())
        {
            IQueryable<Issue> queryable = await _issueRepository.GetQueryableAsync();
            var issue = queryable.FirstOrDefaultAsync(i => i.Title == "My issue title");
            issue.ShouldNotBeNull();
            await uow.CompleteAsync();
        }
    }
}
```

We've used the `IUnitOfWorkManager` service to create a unit of work scope, then called the `FirstOrDefaultAsync` method inside that scope, so we don't have the problem anymore.