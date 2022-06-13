---
layout: default
title: Convert
nav_order: 1
parent: Value Converter
grand_parent: Plugins
---

The Convert method converts the specified value into a different value.

## Syntax
```csharp
public object Convert(object value, DataRow row)
```

## Parameters
*value*
The value to convert. If the field is a calculated field, null is passed since the value to convert will likely come from other columns in row.

*row*
The row in the result set the value is from. This is useful if the values of other columns are used by the converter.

## Return value
The converted value.

## Example
This example, taken from the built-in NumericToDateValueConverter, converts a numeric value to a date and vice versa.

```csharp
using System;
using System.Collections.Generic;
using HorizonReports.Plugins;
using HorizonReports.DataDictionary;
using System.Collections;
using System.Globalization;
using HorizonReports;
using HorizonReports.DataEngine;

namespace HorizonReports.ValueConverters
{
    /// <summary>
    /// Value converter for numeric (YYYYMMDD) to DateTime
    /// </summary>
    [ValueConverterPlugin("{B92E62F2-D603-446A-B840-B5CD86C2A487}",
        "NumericToDateValueConverter",
        PluginSource.Stock,
        typeof(int),
        typeof(DateTime))]
    public class NumericToDateValueConverter :
        IValueConverterPlugin
    {
        // This is not a list type.
        public bool IsListType()
        {
            return false;
        }

        /// <summary>
        /// The field being converted.
        /// </summary>
        public Field Field { get; set; }

        /// <summary>
        /// Not used for this plugin
        /// </summary>
        public string DatasourceName { get; set; }

        /// <summary>
        /// Not used for this plugin
        /// </summary>
        public IDataEngine DataEngine { get; set; }

        /// <summary>
        /// A reference to the report being run.
        /// </summary>
        public IReport Report { get; set; }

        /// <summary>
        /// A list of aliases for the fields that have been retrieved
        /// from the database. If it was necessary to rename a field
        /// this list will contain the corresponding column name for
        /// that field in the passed-in DataRow.
        /// </summary>
        public Dictionary<Field, string> AliasList { get; set; }

        /// <summary>
        /// A reference to the Application object.
        /// </summary>
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        /// <summary>
        /// Convert from the numeric value to DateTime.
        /// </summary>
        public object Convert(object value, System.Data.DataRow row)
        {
            DateTime returnValue = DateTime.MinValue;
            if (value != null)
            {
                string inputValue = value.ToString();
                if (inputValue.Length == 8)
                {
                    inputValue = inputValue.Substring(0, 4) + "-" +
                        inputValue.Substring(4, 2) + "-" +
                        inputValue.Substring(6, 2);
                    if (!DateTime.TryParseExact(inputValue,
                        "yyyy-MM-dd",
                        CultureInfo.InvariantCulture,
                        DateTimeStyles.None, out returnValue))
                    {
                        returnValue = DateTime.MinValue;
                    }
                }
            }
            return returnValue;
        }

        /// <summary>
        /// Convert the DateTime value back into an int.
        /// </summary>
        public object ConvertBack(object value)
        {
            int returnValue;
            if (value == null)
            {
                returnValue = 0;
            }
            else
            {
                DateTime dtValue = (DateTime)value;
                returnValue = dtValue.Year * 10000 +
                    dtValue.Month * 100 +
                    dtValue.Day;
            }
            return returnValue;
        }

        // GetConvertedValuesList returns an empty list.
        public IList GetConvertedValuesList(IField field)
        {
            return new List<string>();
        }

        // Reset does nothing.
        public void Reset()
        {
        }
        /// <summary>
        /// A reference to the report being run.
        /// </summary>
        public IReport Report { get; set; }
    }
}
```
