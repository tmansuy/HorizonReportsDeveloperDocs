---
layout: default
title: BeforeExportReport
nav_order: 9
parent: Report Engine
grand_parent: Plugins
---

The BeforeExportReport method is called just before a report is exported to a file or stream.

## Syntax
```csharp
public bool BeforeExportReport(IReport report, Stream stream)

public bool BeforeExportReport(IReport report, string fileName)
```

## Parameters
*report*
The report being run.

*stream*
The stream the report is being exported to.

*fileName*
The name of the file the report is being exported to.

## Return value
True if the report should be exported, False if not. If you want a message displayed to the user about why it terminated, throw an exception with the appropriate message.

## Example
See the example for [AfterReportSaved](vfps://Topic/_43E0SK68Z).
