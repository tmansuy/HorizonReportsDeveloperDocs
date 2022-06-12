---
layout: default
title: CanUserAccessReport
nav_order: 14
parent: Report Engine
grand_parent: Plugins
---

CanUserAccessReport provides yet another layer of security over which user can access which reports. Using this method, you can prevent a user from seeing a report they may otherwise be able to see. For example, in a hosted solution, you might want users to only see reports they or the ADMIN user created, so they don't even know other users have created reports.

This method is called when accessing the report collection, whether via indexer (by name, ID, or index) or by a LINQ query.

## Syntax
```csharp
public bool CanUserAccessReport(IReportBase report)
```

## Parameters
*report*
The report being checked.

## Return value
True if the user can access the report or false if not.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that only allows a user to see reports they or the ADMIN user created.

```csharp

/// <summary>
/// Returns true if the user can access the specified report. In this
// sample, we only want the user to see reports they created or were
/// created by ADMIN.
/// </summary>
/// <param name="report">
/// The report to check.
/// </param>
/// <returns>
/// True if the user can access the specified report.
/// </returns>
public bool CanUserAccessReport(IReportBase report)
{
    string user = Application.Security.CurrentUser.Name.ToUpper();
    string createdBy = report.Owner.ToUpper();
    bool result = user == "ADMIN" || createdBy == user ||
        createdBy == "ADMIN";
    if (!result)
    {
        Application.Logger.InfoFormat("Report {0} is not accessible to this user",
            report.Name);
    }
    return result;
}
```
