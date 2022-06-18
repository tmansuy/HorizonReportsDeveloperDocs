---
layout: default
title: Convert Back
nav_order: 2
parent: Value Converter
grand_parent: Plugins
---

The ConvertBack method converts the specified value into a different value. This is used when filtering on a field to convert the value the end-user enters into the correct value for the WHERE clause of a SQL statement.

## Syntax
```csharp
public object ConvertBack(object value)
```

## Parameters
*value*
The value to convert.

## Return value
The converted value.

## Example
See the ConvertBack method of the sample code in the [Convert topic]({% link _docs/plugins/valueconverter/convert.md %}).
