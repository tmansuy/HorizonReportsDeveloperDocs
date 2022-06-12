---
layout: default
title: PerformLinkAction
nav_order: 1
parent: Link Action
grand_parent: Plugins
---

The PerformLinkAction method performs the desired action when the user clicks a field in a report.

## Syntax
```csharp
public void PerformLinkAction(object value,
    IReport report,
    System.Data.DataTable data)
```

## Parameters
*value*
The value of the clicked field. For example, if the user clicks "San Francisco," the value of this parameter is "San Francisco."

*report*
The current report.

*data*
The data table for the current report.

## Return value
None.
