---
layout: default
title: AfterReportDeleted
nav_order: 4
parent: Report Engine
grand_parent: Plugins
---

AfterReportDeleted is called after a report has been deleted, even if the deletion failed.

## Syntax
```csharp
public void AfterReportDeleted(IReportBase report, bool reportWasDeleted)
```

## Parameters
*report*
The report that was deleted.

*reportWasDeleted*
True if the report was deleted, false if not.

## Return value
None.

## Example
See the example for [AfterReportSaved](vfps://Topic/_43E0SK68Z).
