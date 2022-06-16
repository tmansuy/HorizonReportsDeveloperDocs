---
layout: default
title: Value Converter
nav_order: 11
has_children: true
parent: Plugins
---

Sometimes, the way a value is stored in a database isn't the way the user expects to see the value in a report. Using a value converter plugin allows you to convert the values stored to the values to display. For example, Sage 300 ERP, an accounting application, stores dates as numeric values; January 10, 2013 is stored as 20130110. The end-user expects to see the date as 01/10/2013 (or however their settings are configured to display dates). The built-in NumericToDateValueConverter converts a numeric value to the corresponding date value. Other built-in converters are:

* *ExcelDateToDateValueConverter*: converts a numeric value using Microsoft Excel's scheme (1 = January 1, 1990) to the corresponding date value.

* *LookupFieldConverter*: looks up a value in another table and displays a field from that table. This is similar to the *Display field from related table* feature but doesn't require a relationship between the tables.

* *StringToDateTimeValueConverter*: converts a string stored in one of several formats into the corresponding date value.

* *StringToNumericValueConverter*: converts a numeric value stored as a string to a numeric value.

* *NumericToBoolValueConverter*: converts a numeric value to true (any value but 0) or false (0).

* *TFToBoolValueConverter*: converts "T" to true and "F" to false.

* *YNToBoolValueConverter*: converts "Y" to true and "N" to false.

* *DisplayFieldFromRelatedTableConverter*: used when you configure a field to display another field from a related table in the Special page of the [properties pane]({% link _docs/studio/datadictionary/field-properties.md %}) for the field. This converter doesn't appear in the list of value converters in the Calc page.

* *EnumeratedFieldValueConverterInt32*: used when you specify that an Int32 field contains enumerated values in the Special page of the [properties pane]({% link _docs/studio/datadictionary/field-properties.md %}) for the field. This converter doesn't appear in the list of value converters in the Calc page.

* *EnumeratedFieldValueConverterString*: like EnumeratedFieldValueConverterInt32, but used when you specify that a String field contains enumerated values.

You specify a value converter for a field by choosing it from the *Value converter* drop-down list in the Calc page of the [field properties editor]({% link _docs/studio/datadictionary/field-properties.md %}) for the field. That list shows the built-in value converter plugins plus any plugins contained in DLLs you put in the Plugins folder of the project. When data is retrieved from the database, the report writer calls the Convert method of the value converter for each field in each row of the result set to convert the value as necessary. When the user creates a filter for a field, the report writer calls the ConvertBack method of the value converter to convert the filter value to the expected value for the WHERE clause.

A value converter plugin implements the *IValueConverterPlugin* interface and uses the ValueConverterPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### IValueConverterPlugin
Here's the definition of IValueConverterPlugin:

```csharp
using System.Collections;
using HorizonReports.DataDictionary;
using HorizonReports.DataEngine;
using System.Data;
using HorizonReports.ReportEngine;
using System.Collections.Generic;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Value Converter plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an
    /// attribute that implements
    /// IValueConverterPluginMetaData.
    /// </remarks>
    public interface IValueConverterPlugin : IBasePlugin
    {
        /// <summary>
        /// A reference to the field this is a converter for.
        /// </summary>
        Field Field { get; set; }

        /// <summary>
        /// A reference to the DataEngine which could be used to
        /// retrieve data needed by the converter.
        /// </summary>
        IDataEngine DataEngine { get; set; }

        /// <summary>
        /// A reference to the report being run.
        /// </summary>
        IReport Report { get; set; }

        /// <summary>
        /// A list of aliases for the fields that have been retrieved
        /// from the database. If it was necessary to rename a field
        /// this list will contain the corresponding column name for
        /// that field in the passed-in DataRow.
        /// </summary>
        Dictionary<Field, string> AliasList { get; set; }

        /// <summary>
        /// The name of the data source Stonefield Query is currently
        /// connected to. This is useful for cases where the converter
        /// needs to call back in to the data engine to retrieve data.
        /// </summary>
        string DatasourceName { get; set; }

        /// <summary>
        /// Converts the specified value from the database to the value
        /// to be displayed.
        /// </summary>
        /// <param name="value">
        /// The value to convert.
        /// </param>
        /// <param name="row">
        /// The row in the result set the value is from. This is useful
        /// if the values of other columns are used by the converter.
        /// </param>
        /// <returns>
        /// The converted value.
        /// </returns>
        object Convert(object value, DataRow row);

        /// <summary>
        /// Converts the specified display value to the value for a
        /// WHERE clause.
        /// </summary>
        /// <param name="value">
        /// The value to convert back.
        /// </param>
        /// <returns>
        /// The converted value.
        /// </returns>
        object ConvertBack(object value);

        /// <summary>
        /// Returns true if this converter contains its own list
        /// of values.
        /// </summary>
        /// <returns>
        /// True if this converter contains its own list of values.
        /// </returns>
        bool IsListType();

        /// <summary>
        /// Returns a list of values (only called if IsListType
        /// returns true).
        /// </summary>
        /// <returns>
        /// A list of possible values for this converter.
        /// </returns>
        IList GetConvertedValuesList();

        /// <summary>
        /// Resets the converter.
        /// </summary>
        void Reset();
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

### ValueConverterPlugin
The ValueConverterPlugin attribute on the plugin class has the following parameters (see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details on all but the two parameters):

* The ID for the plugin.

* The name of the plugin.

* The type of plugin.

* The type for the source data.

* The type for the converted data.

Here's an example:

```csharp
[ValueConverterPlugin("{B92E62F2-D603-446A-B840-B5CD86C2A487}",
    "NumericToDateValueConverter",
    PluginSource.Stock,
    typeof(int),
    typeof(DateTime))]
public class NumericToDateValueConverter :
    IValueConverterPlugin
```

### Plugin properties
Value converter plugins have the following properties:

<table class="detailtable table-striped">
<tr><th>Property</th><th>Type</th><th>Purpose</th>
</tr>
<tr>
<td>DataEngine</td>
<td>IDataEngine</td>
<td>A reference to the DataEngine object that called the converter. This can be used to access the database if necessary.</td>
</tr>
<tr>
<td>DatasourceName</td>
<td>string</td>
<td>The name of the current data source. This may be important for data source-specific conversions.</td>
</tr>
<tr>
<td>Field</td>
<td>Field</td>
<td>The field the converter is being applied to. The field's PluginData property may contain information the converter needs.</td>
</tr>
<tr>
<td>Report</td>
<td>IReport</td>
<td>A reference to the report being run. This can be used to check the names of the fields in the result set if necessary.</td>
</tr>
</table>
