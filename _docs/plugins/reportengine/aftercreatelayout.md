---
layout: default
title: AfterCreateLayout
nav_order: 1
parent: Report Engine
grand_parent: Plugins
---

AfterCreateLayout is called right after the layout of a report has been generated. It allows you to modify the layout as necessary.

## Syntax
```csharp
public bool AfterCreateLayout(IReport report)
```

## Parameters
*report*
The report being run.

## Return value
True if the layout process can continue, false if not. If you want a message displayed to the user about why it terminated, throw an exception with the appropriate message.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that removes column headings from the data-only layout so they aren't exported to CSV or Microsoft Excel.

```csharp
/// <summary>
/// Executes just after the layout for the specified report is created.
// In this case, we'll remove the column headings from the data-only
/// layout so they aren't exported to CSV or Microsoft Excel.
/// </summary>
/// <param name="report">
/// The report being run.
/// </param>
/// <returns>
/// True if the layout process can continue, false if not.
/// </returns>
public bool AfterCreateLayout(IReport report)
{
    ReportLayout layout = (ReportLayout)report.ReportLayoutDataOnly;
    Band pageHeader = layout.Bands.GetBandByType(typeof(PageHeaderBand));
    if (pageHeader != null)
    {
        layout.Bands.Remove(pageHeader);
    }
    return true;
}
```
