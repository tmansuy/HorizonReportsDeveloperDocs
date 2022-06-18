---
layout: default
title: GetVersion
nav_order: 3
parent: Data Dictionary
grand_parent: Plugins
---

If you use [versioning]({% link _docs/studio/datadictionary/versioning.md %}) in your data dictionary, you need a way to determine the version number of a specific object in the currently selected database. The GetVersion methods of a data dictionary plugin is the means. These methods are called when a field, table, or join is retrieved from the indexer of the appropriate collection. If the object should be hidden because of versioning issues, the indexer returns null, acting as if the object doesn't exist.

## Syntax
```csharp
public string GetVersion(Table item)
public string GetVersion(Field item)
public string GetVersion(Join item)
```

## Parameters
The table, field, or join being checked for version.

## Return value
The version number of the object as a string or a blank string if there is no version number.

> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> For performance reasons, you'll likely want to look up the version information once, cache it, and use the cached value the next time the method is called. One thing that complicates this is that each data source may have its own version information, so you should store and look up the cache by data source. The sample code below shows an example of how to do that.

## Example
Suppose the first two characters of the table name represent the module the table belongs to (for example, ARCUS is the customers table in the AR, or Accounts Receivable, module). Also suppose a table named CSAPP contains the version number of each module. The following code returns the version number from the current database for the module the specified table, field, or join belongs to.

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

        public void AfterLoaded()
        {
        }

        /// <summary>
        /// Get the version number for the module the field is in
        /// (the first two characters of the table name).
        /// </summary>
        public string GetVersion(Field item)
        {
            string module = item.Table.Name.Substring(0, 2);
            return GetModuleVersion(module);
        }

        /// <summary>
        /// Get the version number for the module the table is in
        /// (the first two characters of the table name).
        /// </summary>
        public string GetVersion(Table item)
        {
            string module = item.Name.Substring(0, 2);
            return GetModuleVersion(module);
        }

        /// <summary>
        /// Get the version number for the module the join is in
        /// (the first two characters of the child table name).
        /// </summary>
        public string GetVersion(Join item)
        {
            string module = item.ChildTable.Name.Substring(0, 2);
            return GetModuleVersion(module);
        }

        /// <summary>
        /// A cache of the CSAPP table by data source name.
        /// </summary>
        private Dictionary<string, DataTable> _versionCache =
            new Dictionary<string, DataTable>();

        /// <summary>
        /// Get the version for the specified module from the
        /// current data source.
        /// </summary>
        private string GetModuleVersion(string module)
        {
            // Get the current datasource.
            IDataSource ds = Application.ConnectionManager.DataSources.CurrentDatasource;
            DataTable versionCheck;
            try
            {
                // See if we have a cached DataTable for it.
                versionCheck = _versionCache[ds.Name];
            }
            catch
            {
                // We don't have a cached copy, so get a connection
                // object, retrieve the CSAPP table, and add it to
                // the cache.
                Database database = DataDictionary.Databases[0];
                IConnectionFactory factory = ds.GetConnection(database.Name)
                    as IConnectionFactory;
                IConnection conn = factory.CreateConnection();
                versionCheck = conn.ExecuteSQLStatement("select PGMID, PGMVER from CSAPP",
                    null, "CSAPP");
                _versionCache.Add(ds.Name, versionCheck);
            }

            // Find the module record and get its version number.
            DataRow[] rows = versionCheck.Select("PGMID='" +
                module + "'");
            string version = rows[0]["PGMVER"].ToString();
            return version;
        }
    }
}
```
