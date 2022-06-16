---
layout: default
title: BeforeReportCopied
nav_order: 10
parent: Report Engine
grand_parent: Plugins
---

BeforeReportCopied is called before a report is copied.

## Syntax
```csharp
public bool BeforeReportCopied(IReportBase report, string name)
```

## Parameters
*report*
The report that was copied.

*name*
The name for the copy.

## Return value
True if the report should be copied, false if not.

## Example
See the example for [AfterReportSaved]({% link _docs/plugins/reportengine/afterreportsaved.md %}).
