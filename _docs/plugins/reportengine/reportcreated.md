---
layout: default
title: ReportCreated
nav_order: 15
parent: Report Engine
grand_parent: Plugins
---

The ReportCreated method allows you to change something about the report immediately after it's created.

## Syntax
```csharp
public void ReportCreated(IReportBase report)
```

## Parameters
*report*
The new report.

## Return value
None.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that removes the automatically-added permission for Everyone so by default, only the user creating the report has access to it.

```csharp
/// <summary>
/// Executes when a report is created. In this case, we'll remove the
/// automatically-added permission for Everyone so by default, only the
/// user creating the report has access to it.
/// </summary>
/// <param name="report">
/// The new report.
/// </param>
public void ReportCreated(IReportBase report)
{
    report.RemovePermission(
        new Permission(Application.Security.EveryoneRole,
        AccessRights.Full));
}
```
