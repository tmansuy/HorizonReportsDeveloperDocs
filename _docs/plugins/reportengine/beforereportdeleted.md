---
layout: default
title: BeforeReportDeleted
nav_order: 11
parent: Report Engine
grand_parent: Plugins
---

BeforeReportDeleted is called before a report is deleted.

## Syntax
```csharp
public bool BeforeReportDeleted(IReportBase report)
```

## Parameters
*report*
The report to be deleted.

## Return value
True if the report should be deleted, false if not.

## Example
See the example for [AfterReportSaved](vfps://Topic/_43E0SK68Z).
