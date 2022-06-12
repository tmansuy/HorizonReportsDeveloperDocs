---
layout: default
title: BeforeCreateLayout
nav_order: 7
parent: Report Engine
grand_parent: Plugins
---

The BeforeCreateLayout method allows you to change something about the report before the layout used to render the report is generated.

## Syntax
```csharp
public bool BeforeCreateLayout(IReport report)
```

## Parameters
*report*
The report being run.

## Return value
True if the report run should continue, False if it should terminate. If you want a message displayed to the user about why it terminated, throw an exception with the appropriate message.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that forces the template for the report to Elegant.

```csharp
/// <summary>
/// Executes just before the layout for the specified report is created.
/// In this case, we'll force the template for the report to Elegant.
/// </summary>
/// <param name="report">
/// The report being run.
/// </param>
/// <returns>
/// True if the layout process can continue, false if not.
/// </returns>
public bool BeforeCreateLayout(IReport report)
{
    report.Template = Application.ReportEngine.Templates["Elegant"];
    return true;
}
```
