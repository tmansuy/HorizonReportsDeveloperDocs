---
layout: default
title: AfterDataRetrieved
nav_order: 2
parent: Report Engine
grand_parent: Plugins
---

AfterDataRetrieved is called after the data has been retrieved for a report (the ResultSet property of the report contains the DataTable for the report) but before the report layout has been created. This method can be used to do anything at this stage in the report run, such as modifying the data in the result set.

Here's one use for this method. Horizon Reports has built-in field-level security; by specifying which roles can access a field, you can ensure that certain users can't see the values in that field, such as employee salary. However, that means a user who can't access a field can't run any report using that field. Suppose you want the user to be able to run such a report but not see the data for that field. In that case, the code in the AfterDataRetrieved method can blank the contents of fields the user shouldn't see.

## Syntax
```csharp
public bool AfterDataRetrieved(IReport report, IDataEngine dataEngine)
```

## Parameters
*report*
The report being run.

*dataEngine*
A data engine object used to retrieve data.

## Return value
True if the report run should continue, False if it should terminate. If you want a message displayed to the user about why it terminated, throw an exception with the appropriate message.

## Example
Here's an example, an excerpt from SampleReportEnginePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, that nulls the HireDate field if that field is in the report and the current user isn't an administrator to prevent them from seeing the value.

```csharp
/// <summary>
/// Executes just after the data for the specified report is retrieved.
/// In this case, we'll null the HireDate field if that field is in the
/// report and the current user isn't an administrator to prevent them
/// from seeing the value.
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
/// <remarks>
/// The ResultSet property of the report contains the DataTable used
/// for the report.
/// </remarks>
public bool AfterDataRetrieved(IReport report, IDataEngine dataEngine)
{
    if (!Application.Security.IsCurrentUserInRole(new List<IRole>()
        { Application.Security.AdministratorRole }))
    {
        var fields = report.GetFields();
        IField field =
            Application.DataDictionary.Fields["Employees.HireDate"];
        var reportField = fields.Where(f => f.Field ==
            field).FirstOrDefault();
        if (reportField != null)
        {
            string fieldName = reportField.ResultSetFieldName;
            foreach (DataRow row in report.ResultSet.Rows)
            {
                row[fieldName] = DBNull.Value;
            }
        }
    }
    return true;
}
```
