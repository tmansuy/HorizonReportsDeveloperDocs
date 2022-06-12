---
layout: default
title: BeforeDataRetrieved
nav_order: 8
parent: Report Engine
grand_parent: Plugins
---

BeforeDataRetrieved is called before the data has been retrieved for a report. This method can be used to do anything at this stage in the report run, such as modifying the report's fields or filter conditions.

## Syntax
```csharp
public bool BeforeDataRetrieved(IReport report, IDataEngine dataEngine)
```

## Parameters
*report*
The report being run.

*dataEngine*
A data engine object used to retrieve data.

## Return value
True if the report run should continue, False if it should terminate. If you want a message displayed to the user about why it terminated, throw an exception with the appropriate message.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that adds filter conditions of Orders.EmployeeID = 1 and Orders.OrderDate is between 01/01/2015 and 12/31/2015 to any report containing a field from the Orders table. Because the Visible property of the FilterCondition objects is set to false, these conditions don't appear in the report wizard so the user doesn't know they're there.

```csharp
/// <summary>
/// Executes just before the data for the specified report is retrieved.
/// In this case, we'll add another filter condition to the report: if
/// the report is showing orders, we'll only allow the user to see orders
/// they were the salesperson for (in this sample, we'll just hard-code
/// it to employee number 1) and in the year 2015.
/// </summary>
/// <param name="report">
/// The report being run.
/// </param>
/// <param name="dataEngine">
/// The data engine being used to retrieve the data.
/// </param>
/// <returns>
/// True if the report run can continue, false if not.
/// </returns>
public bool BeforeDataRetrieved(IReport report, IDataEngine dataEngine)
{
    var fields = report.GetFields();
    Table table = Application.DataDictionary.Tables["Orders"];
    bool orders = fields.Any(f => f.Field.Table == table);
    if (orders)
    {
        Field field =
            Application.DataDictionary.Fields["Orders.EmployeeID"];
        IFilterCondition condition = report.FilterConditions.New(field);
        condition.DisplayCondition = false;
        condition.Values.Add(1);
        condition.Visible = false;

        field = Application.DataDictionary.Fields["Orders.OrderDate"];
        condition = report.FilterConditions.New(field);
        condition.Operator = new OperatorBetween();
        condition.Connection = new AndConnection();
        condition.DisplayCondition = false;
        condition.Values.Add(new DateTime(2015, 1, 1));
        condition.Values.Add(new DateTime(2015, 12, 31));
        condition.Visible = false;
    }
    return true;
}
```
