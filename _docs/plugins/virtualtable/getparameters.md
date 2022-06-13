---
layout: default
title: GetParameters
nav_order: 1
parent: Virtual Table
grand_parent: Plugins
---

If the Select method needs some parameter values, such as if it calls a stored procedure and that stored procedure has parameters, and you want to ask the user for the values of those parameters, have the GetParameters method return a list of IParameter objects for those parameters. The user is prompted for values for these parameters and the Select method can use the Parameters collection of the report to get the values the user entered. If desired, you can populate the AvailableValues collection of the Parameter class with options for user selection, and the UI will present those as optional values for the parameter.

If you don't need to prompt the user for value, have this method return an empty list; that is:

```csharp
return new List<IParameter>();
```

## Syntax
```csharp
public List<IParameter> GetParameters(Table table)
```

## Parameters
*table*
The table the plugin is for.

## Return value
A list of IParameter objects for the parameters you want the user to be prompted for.

## Example
This example creates a Category parameter with a pre-defined list of values the user can choose from.

```csharp
public List<IParameter> GetParameters(ITable table)
{
    List<IParameter> parameters = new List<IParameter>();
    IParameter parameter = new Parameter();
    parameter.Name = "Category";
    parameter.Type = typeof(System.String);
    parameter.Caption = "Category";
    parameter.AvailableValues.Add("Beverages");
    parameter.AvailableValues.Add("Condiments");
    parameter.AvailableValues.Add("Confections");
    parameters.Add(parameter);
    return parameters;
}
```
