---
layout: default
title: GetConvertedValuesList
nav_order: 3
parent: Value Converter
grand_parent: Plugins
---

The [IsListType](vfps://Topic/_3QW0RCQQR) method determines whether the value converter maintains a list of possible values. If it returns true, the GetConvertedValuesList method is used to get a list of values to display to the user when the Values button is pressed. If it returns false, the report writer does the usual mechanism to get the values: either using a [values method plugin](vfps://Topic/_3QW0STVGI) for the field or using a SELECT DISTINCT SQL statement.

## Syntax
```csharp
public IList GetConvertedValuesList(Field field)
```

## Parameters
*field*
The field the value converter is operating on.

## Return value
A list of values for the field.

## Example
This example is taken from EnumeratedFieldValueConverterString, one of the built-in value converters. It's used when you specify that a String field contains enumerated values in the Special page of the [properties pane](vfps://Topic/_0OY0TQXLS) for the field. (Not all the code for the class is shown here, only the relevant parts.) When the DataEngine sets the Field property for the converter, the getter for that property calls LoadPluginData to load an XmlDocument object with the contents of the PluginData property of the field. Here's an example of what that property contains (automatically filled in by Horizon Reports Studio from the values you enter in the values list):

    <values>
      <value value="1" result="Fedex" />
      <value value="2" result="UPS" />
      <value value="3" result="Mail" />
    </values>

The GetConvertedValuesList method puts the values in the result attribute of that XML into a list.

```csharp
/// <summary>
/// An XmlDocument holding the plugin data for the field.
/// </summary>
protected XmlDocument _doc;

/// <summary>
/// Load an XmlDocument with the field's PluginData.
/// </summary>
private void LoadPluginData(string pluginData)
{
    _doc = new XmlDocument();
    if (!String.IsNullOrWhiteSpace(pluginData))
    {
        _doc.LoadXml(pluginData);
    }
}

/// <summary>
/// The underlying store for Field.
/// </summary>
protected Field _field;

/// <summary>
/// The field being converted.
/// </summary>
/// <remarks>
/// This converter loads the plugin data into an XmlDocument when the
/// field is specified.
/// </remarks>
public Field Field
{
    get
    {
        return _field;
    }
    set
    {
        _field = value;
        LoadPluginData(value.PluginData);
    }
}

/// <summary>
/// Returns a list of values (only called if IsListType returns true).
/// </summary>
public IList GetConvertedValuesList(Field field)
{
    IList list = new List<string>();
    XmlNodeList idNodes = _doc.SelectNodes("values/value");
    foreach (XmlNode node in idNodes)
    {
        list.Add(node.Attributes["result"]);
    }
    return list;
}
```
