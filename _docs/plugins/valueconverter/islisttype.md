---
layout: default
title: IsListType
nav_order: 4
parent: Value Converter
grand_parent: Plugins
---

IsListType determines whether the value converter maintains a list of possible values. If it returns true, the [GetConvertedValuesList]({% link _docs/plugins/valueconverter/getconvertedvalueslist.md %}) method is used to get a list of values to display to the user when the Values button is pressed. If it returns false, the report writer does the usual mechanism to get the values: either using a [values method plugin]({% link _docs/plugins/valuesmethod/index.md %}) for the field or using a SELECT DISTINCT SQL statement.

## Syntax
```csharp
public bool IsListType()
```

## Parameters
None.

## Return value
True if this value converter has a list of values, false if not.

## Example
See the IsListType method of the sample code in the [Convert help topic]({% link _docs/plugins/valueconverter/convert.md %}).
