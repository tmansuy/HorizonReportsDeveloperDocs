---
layout: default
title: AfterReportSaved
nav_order: 5
parent: Report Engine
grand_parent: Plugins
---

AfterReportSaved is called after a report has been saved.

## Syntax
```csharp
public void AfterReportSaved(IReportBase report)
```

## Parameters
*report*
The report that was saved.

## Return value
None.

## Example
This example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, logs many of the "before" and "after" methods.

```csharp

/// <summary>
/// Executes just before the specified report is exported to a stream.
/// In this case, we'll log the report run.
/// </summary>
/// <param name="report">
/// The report being exported.
/// </param>
/// <param name="stream">
/// The stream.
/// </param>
/// <returns>
/// True if the report should be exported, false if not.
/// </returns>
public bool BeforeExportReport(IReport report, Stream stream)
{
    Application.Logger.InfoFormat("Report {0} was output to a stream at " +
        "{1} by {2}", report.Name, DateTime.Now,
        Application.Security.CurrentUser.Name);
    return true;
}

/// <summary>
/// Executes just before the specified report is exported to a file.
/// In this case, we'll log the report run.
/// </summary>
/// <param name="report">
/// The report being exported.
/// </param>
/// <param name="fileName">
/// The name of the file.
/// </param>
/// <returns>
/// True if the report should be exported, false if not.
/// </returns>
public bool BeforeExportReport(IReport report, string fileName)
{
    Application.Logger.InfoFormat("Report {0} was output to {1} at {2} " +
        "by {3}", report.Name, fileName, DateTime.Now,
        Application.Security.CurrentUser.Name);
    return true;
}

/// <summary>
/// Executes just after the specified report is saved. In this case,
/// we'll log it.
/// </summary>
/// <param name="report">
/// The report being saved.
/// </param>
public void AfterReportSaved(IReportBase report)
{
    Application.Logger.InfoFormat("Report {0} was saved at {1}", report.Name,
        DateTime.Now);
}

/// <summary>
/// Executes just before the specified report is copied. We're
/// doing nothing in this example.
/// </summary>
/// <param name="report">
/// The report being copied.
/// </param>
/// <param name="name">
/// The name to assign to the copy.
/// </param>
/// <returns>
/// True if the report should be copied, false if not.
/// </returns>
public bool BeforeReportCopied(IReportBase report, string name)
{
    Application.Logger.InfoFormat("Report {0} is about to be copied to " +
        "{1} at {2}", report.Name, name, DateTime.Now);
    return true;
}

/// <summary>
/// Executes just after the specified report is copied. In this case,
/// we'll log it.
/// </summary>
/// <param name="report">
/// The report being copied.
/// </param>
/// <param name="copy">
/// The copied report.
/// </param>
public void AfterReportCopied(IReportBase report, IReportBase copy)
{
    Application.Logger.InfoFormat("Report {0} was copied to {1} at {2}",
        report.Name, copy.Name, DateTime.Now);
}

/// <summary>
/// Executes just before the specified report is deleted. We're doing
/// nothing in this example.
/// </summary>
/// <param name="report">
/// The report being deleted.
/// </param>
/// <returns>
/// True if the report should be deleted, false if not.
/// </returns>
public bool BeforeReportDeleted(IReportBase report)
{
    Application.Logger.InfoFormat("Report {0} is about to be deleted", report.Name);
    return true;
}

/// <summary>
/// Executes just after the specified report is deleted. In this case,
/// we'll log it.
/// </summary>
/// <param name="report">
/// The report being deleted.
/// </param>
/// <param name="reportWasDeleted">
/// True if the report was deleted.
/// </param>
public void AfterReportDeleted(IReportBase report, bool reportWasDeleted)
{
    if (reportWasDeleted)
    {
        Application.Logger.InfoFormat("Report {0} was deleted at {1}",
            report.Name, DateTime.Now);
    }
}
```
