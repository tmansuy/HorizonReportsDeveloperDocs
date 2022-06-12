---
layout: default
title: BeforeReportSaved
nav_order: 12
parent: Report Engine
grand_parent: Plugins
---

The BeforeReportSaved method is called just before a report is saved. It allows you to change something about the report before it's written to an SFX file.

## Syntax
```csharp
public void BeforeReportSaved(IReportBase report)
```

## Parameters
*report*
The report being saved.

## Example
This example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, ensures the report uses a tag with the user's name in it. If such a tag doesn't exist, it's created.

```csharp
/// <summary>
/// Executes just before the specified report is saved. In this case,
/// we'll make sure the report uses a tag with the user's name in it.
/// </summary>
/// <param name="report">
/// The report being saved.
/// </param>
public void BeforeReportSaved(IReportBase report)
{
    // First see if the report already has the desired tag.
    string tagName = Application.Security.CurrentUser.Name + "'s Reports";
    bool gotIt = report.Tags.Any(t => t.Name == tagName);
    if (!gotIt)
    {
        // It doesn't so see if the tag exists and add it if not.
        ITag tag = Application.ReportEngine.Tags[tagName];
        if (tag == null)
        {
            tag = Application.ReportEngine.Tags.New(tagName);
            Application.ReportEngine.Tags.SaveItem(tag);
        }

        // Add the tag to the report.
        report.Tags.Add(tag);
    }
}
```
