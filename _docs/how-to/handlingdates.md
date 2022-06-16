---
layout: default
title: Handling Dates Stored as Non-Date Values
nav_order: 8
parent: How To
---

Some applications store dates as non-date values. For example, your application may store a date as an integer that looks like a date, such as 20101215 for December 15, 2010, or perhaps as the number of seconds after midnight. The problem is that doesn't make it very friendly to display to the user and makes it difficult to filter on a date range.

The solution is to convert the value to a true date value using a value converter plugin. A value converter plugin allows you to convert the values stored to the values to display. For example, Sage 300 ERP, an accounting application, stores dates as numeric values; January 10, 2013 is stored as 20130110. The end-user expects to see the date as 01/10/2013 (or however their Windows system is configured to display dates). The built-in NumericToDateValueConverter converts a numeric value to the corresponding date value, while the built-in StringToDateValueConverter converts a string. You can also create your own plugin if necessary. See the [Field Properties]({% link _docs/studio/datadictionary/field-properties.md %}) and [Value Converter]({% link _docs/plugins/valueconverter/index.md %}) topics for more information.