---
layout: default
title: AfterLoaded
nav_order: 1
parent: Data Dictionary
grand_parent: Plugins
---

The AfterLoaded method is intended to be used to customize the data dictionary at runtime. Why not just do this in Horizon Reports Studio? There may be many reasons:

* Perhaps you don't want certain users to access certain tables. In that case, you want to set the Reportable property of the appropriate Table objects to false based on the user name. While you could use [role-based security]({% link _docs/studio/security.md %}) for this, doing it in the AfterLoaded method makes it more dynamic.

* If you allow your users to customize the caption for certain fields, or even add their own custom fields to the tables, you want the report writer to know about the changes the user made.

* If users can purchase your application by module, you don't want those tables belonging to modules the user hasn't purchased listed in the report writer.

This method is called immediately after Horizon Reports loads the collections from the data dictionary database. So, you have full access to the collections without altering the data dictionary database. Note that the data dictionary is loaded before any user logs in, so there's no selected data source yet. If your code needs to access the data source, such as to customize the data dictionary based on some data in the database, use the [AfterLogin]({% link _docs/plugins/application/afterlogin.md %}) method of an application plugin instead.

## Syntax
```csharp
public void AfterLoaded()
```

## Parameters
None.

## Example
Here's an example that adds custom fields the user has added to their tables to the data dictionary. It assumes there's a table called CustomFields in the application's database that defines the custom fields. In this table, the Table column contains the name of the table the field was added to, Name contains the field name, Type contains the data type, and Heading contains the caption for the field.

```csharp
using System.Collections.Generic;
using System.Data;
using HorizonReports;
using HorizonReports.ConnectionManagement;
using HorizonReports.DataDictionary;
using HorizonReports.Plugins;

namespace SamplePlugins
{
    [DataDictionaryPlugin("{815AB23B-403D-418C-A85D-DE8B3B5595FB}",
        "SampleDataDictionaryPlugin",
        PluginSource.Custom,
        Version = "1.0.0.0",
        ExecutionPriority = 5)]
    public class SampleDataDictionaryPlugin :
        IDataDictionaryPlugin
    {
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        public IDataDictionary DataDictionary { get; set; }

        /// <summary>
        /// Add custom fields defined in the CustomFields table
        /// to the data dictionary.
        /// </summary>
        public void AfterLoaded()
        {
            // Get a connection object for the current datasource.
            IDataSource ds = Application.ConnectionManager.DataSources.CurrentDatasource;
            Database database = Application.DataDictionary.Databases[0];
            IConnectionFactory factory = ds.GetConnection(database.Name)
                as IConnectionFactory;
            IConnection conn = factory.CreateConnection();

            // Get the CustomFields table.
            DataTable result = conn.ExecuteSQLStatement("select * from CustomFields",
                null, "CustomFields");

            // Add each custom field to the data dictionary.
            foreach (DataRow row in result.Rows)
            {
                string tableName = row["Table"].ToString();
                Table table = Application.DataDictionary.Tables[tableName];
                string fieldName = row["Name"].ToString();
                Field field = Application.DataDictionary.Fields.New(tableName +
                    "." + fieldName);
                field.Caption = row["Heading"].ToString();
                field.DataType = System.Type.GetType(row["Type"].ToString());
                field.Table = table;
            }
        }

        public void BeforeLoaded()
        {
        }

        public string GetVersion(Field item)
        {
            return "";
        }

        public string GetVersion(Table item)
        {
            return "";
        }

        public string GetVersion(Join item)
        {
            return "";
        }
    }
}
```
