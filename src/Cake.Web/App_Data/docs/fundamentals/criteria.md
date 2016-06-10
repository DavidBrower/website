---
content-type: markdown
---

You can control and influence the flow of the build script execution by providing criteria. This is a predicate that has to be fulfilled for the task to execute. The criteria does not affect how the succeeding task will be executed.

```csharp
Task("A")
    .WithCriteria(DateTime.Now.Second % 2 == 0)
    .Does(() =>
{
});

Task("B")
    .WithCriteria(() => DateTime.Now.Second % 2 == 0)
    .IsDependentOn("A")
    .Does(() =>
{
});

RunTarget("B");
```

Task `A`'s criteria will be set when the task is created while Task `B`'s criteria will be evaluated when the task is being executed.

For criteria with states that might change during the execution of the build script, consider using the lambda alternative.
