---
layout: default
title: Data Engine
nav_order: 6
has_children: true
parent: Plugins
---

A database defined in the data dictionary is a logical database: it defines what tables belong to the database and the structure of those tables. A physical database is the actual database on disk. The logical database doesn't concern itself with connection information; those are issues for the physical database. For example, you may have both SQL Server and SQLite versions of the same logical database; the Northwind sample database that comes with both of these is one such set of physical databases that have the same logical database structure.

A Database object in the data dictionary contains information about a logical database. A DataSource object defines the connection information for a physical database.

Data engine plugins can be used to specify the list of data sources the user can query on. For example, your application may use a configuration file that lists the data sources and their connection settings. A data engine plugin can read the same configuration file to create the data sources the report writer can access.

A data engine plugin implements the IDataEnginePlugin interface uses the DataEnginePlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

## IDataEnginePlugin
Here's the definition of IDataEnginePlugin:

```csharp
using System;
using System.Diagnostics.Contracts;
using HorizonReports.ConnectionManagement;
&nbsp;
namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Data Engine plugins must implement.
    /// </summary>
    public interface IDataEnginePlugin :
        IBasePlugin
    {
        /// <summary>
        /// Fills the specified collection with data sources the
        /// user can query on.
        /// </summary>
        bool GetDataSources(IDataSourceCollection dataSources);

        /// <summary>
        /// Returns the name of the current data source used for reports.
        /// </summary>
        string GetCurrentDataSource(IDataSourceCollection dataSources);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

## DataEnginePlugin
The DataEnginePlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details. Here's an example:

```csharp
[DataEnginePlugin("{FB22E1B5-9AA1-4CE1-9D16-AEFDF0FB6E6C}",
    "SampleDataEnginePlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleDataEnginePlugin :
    IDataEnginePlugin
```