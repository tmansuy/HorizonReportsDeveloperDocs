---
layout: default
title: Select
nav_order: 2
parent: Virtual Table
grand_parent: Plugins
---

The Select method does whatever is necessary to create a DataTable for the virtual table the plugin is for. It could, for example, retrieve data from current and archived invoice tables in the database and combine them into a single DataTable, which would be easier for the end-user to report on than two separate tables. It could call a web service that returns currency exchange rates. Horizon Reports doesn't care what the plugin does, as long as it returns a DataTable.

If the code in the Select method performs a parameterized query, typically by calling the ExecuteSQLStatement method of the specified connection object, you can specify the values for those parameters a couple of ways:

* Use a SELECT statement with the WHERE clause populated with the hard-coded values.

* Use a SELECT statement with "?" as placeholders for the values and pass the values to use in the second parameter to ExecuteSQLStatement. See the sample code below for an example.

You can get the values of the parameters from the Parameters collection of the specified report object if you used the GetParameters method to define those parameters (the sample code below does this). Another possibility is to get the values from any ask-at-runtime filter conditions for the report. In that case, go through the FilterConditions property of the specified report, which is a collection of FilterCondition objects, checking whether the condition's Field.Name is the field you're interested in, and if so, get the values the user entered from the Values member, which is an instance of ConditionValues, a collection of ConditionValue objects.

## Syntax
```csharp
public DataTable Select(
    IConnection connection,
    string datasource,
    string select,
    string tablename,
    IReport report,
    ITable table)
```

## Parameters
*connection*
An IConnection object you can use to retrieve data from the database if necessary. See the sample code below for an example.

*datasource*
The name of the data source the report writer is connected to, in case you need that for something.

*select*
The SQL statement Horizon Reports would have sent to the database engine had this been a real table. You may find the statement useful if you need to know, for example, what the WHERE clause is.

*tablename*
The name of the virtual table.

*report*
The report the result is for.

*table*
The table the plugin is for.

## Return value
A DataTable populated with, at a minimum, the columns specified by the SQL statement passed as the third parameter. Having more columns isn't a problem, as only the ones specified appear in the report.

## Example
This example, taken from SampleVirtualTablePlugin.cs of the Samples\SamplePlugins\SamplePlugins folder, is used by the SalesByCategory table in the sample project. This code calls the SalesByCategory stored procedure in the Northwind SQL Server sample database. Note that it returns an empty DataTable if it isn't using the SQL Server database, since that stored procedure doesn't exist in the Microsoft Access version of that database. Note also that it uses the parameters specified in the GetParameters method.

```csharp
using System.Data;
using HorizonReports;
using HorizonReports.ConnectionManagement;
using HorizonReports.Plugins;
using System.ComponentModel.Composition;
using HorizonReports.ReportEngine;
using System.Collections.Generic;
using HorizonReports.DataDictionary;

namespace SamplePlugins
{
    /// <summary>
    /// A plugin that creates the result set for the SalesByCategory
    // table in the sample project.
    /// </summary>
    /// <remarks>
    /// This shows a simple example of how to create a plugin for a
    // virtual table.
    /// </remarks>
    [VirtualTablePlugin("{FC5CDC44-72E7-415F-87F3-CEFB088FF4FE}",
        "SampleVirtualTablePlugin",
        PluginSource.Custom,
        "SalesByCategory",
        Version = "1.0.0.0",
        ExecutionPriority = 5)]
    public class SampleVirtualTablePlugin :
        IVirtualTablePlugin
    {
        /// <summary>
        /// A reference to the Application object in
        // case it's needed.
        /// </summary>
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        /// <summary>
        /// Returns a list of parameters the Select method needs
        /// (typically when it calls a stored procedure). In this case,
        /// we need Category and Year.
        /// </summary>
        /// <param name="table">
        /// The table the plugin is for.
        /// </param>
        /// <returns>
        /// A list of Parameters.
        /// </returns>
        public List<Parameter> GetParameters(Table table)
        {
            List<IParameter> parameters = new List<Parameter>();
            Parameter parameter = new Parameter();
            parameter.Name = "Category";
            parameter.Type = typeof(System.String);
            parameter.Caption = "Category";
            parameter.Value = "Beverages";
            parameters.Add(parameter);

            parameter = new Parameter();
            parameter.Name = "Year";
            parameter.Type = typeof(System.String);
            parameter.Caption = "Year";
            parameter.Value = "1997";
            parameters.Add(parameter);

            return parameters;
        }

        /// <summary>
        /// SalesByCategory shows total sales by product for a specified
        /// year and product category by calling the SalesByCategory
        /// stored procedure in the SQL Server Northwind database.
        /// </summary>
        /// <param name="connection">
        /// The IConnection object that performs the query.
        /// </param>
        /// <param name="datasource">
        /// The name of the datasource connected to (not used in this
        /// example).
        /// </param>
        /// <param name="select">
        /// The SQL statement used by the report (not used in this
        /// example).
        /// </param>
        /// <param name="tablename">
        /// The name of the table being created.
        /// </param>
        /// <param name="report">
        /// The report the result is for.
        /// </param>
        /// <param name="table">
        /// The table the plugin is for.
        /// </param>
        /// <returns>
        /// A DataTable containing the desired results.
        /// </returns>
        /// <remarks>
        /// Note that this code doesn't worry about the WHERE clause
        /// in the SQL statement; the data engine calling this code will
        /// take care of that.
        /// </remarks>
        public DataTable Select(IConnection connection,
            string datasource, string select, string tablename,
            IReport report, Table table)
        {
            // We can only do this if we're connected to the SQL Server
            /// version of Northwind. Also we use default values in case
            /// the report didn't have any parameters.
            DataTable result;
            if (datasource == "Northwind SQL")
            {
                string category = "Beverages";
                string year = "1997";
                IParameter parameter = report.Parameters["Category"];
                if (parameter != null)
                {
                    category = parameter.Value.ToString();
                }
                parameter = report.Parameters["Year"];
                if (parameter != null)
                {
                    year = parameter.Value.ToString();
                }
                result = connection.ExecuteSQLStatement(
                    "exec SalesByCategory ?, ?",
                    new string[] { category, year }, tablename, report);
            }
            else
            {
                result = new DataTable();
            }
            return result;
        }
    }
}
```
