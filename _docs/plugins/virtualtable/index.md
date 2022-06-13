---
layout: default
title: Virtual Table
nav_order: 13
has_children: true
parent: Plugins
---

Since a virtual table doesn't really exist, the report writer can't send a SQL statement to the database engine to retrieve the data for it. Instead, you have to write a plugin to create the result set for the virtual table.

A virtual table plugin implements the [IVirtualTablePlugin](vfps://Topic/Interface%20IStonefieldQueryVirtualTablePlugin) interface and uses the VirtualTablePlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### IVirtualTablePlugin
Here's the definition of IVirtualTablePlugin:

```csharp
using System;
using System.Data;
using HorizonReports.ConnectionManagement;
using HorizonReports.ReportEngine;
using System.Collections.Generic;
using HorizonReports.DataDictionary;
&nbsp;
namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that VirtualTable plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an
    /// attribute that implements
    /// IVirtualTablePluginMetaData.
    /// </remarks>
    public interface IVirtualTablePlugin : IBasePlugin
    {
        /// <summary>
        /// Returns a list of parameters the Select method needs
        /// (typically when it calls a stored procedure).
        /// </summary>
        /// <param name="table">
        /// A reference to the table the plugin is for.
        /// </param>
        /// <returns>
        /// A list of IParameters.
        /// </returns>
        List<IParameter> GetParameters(Table table);

        /// <summary>
        /// Retrieves the data for the virtual table and returns a
        /// DataTable.
        /// </summary>
        /// <param name="connection">
        /// A connection object to use for the data retrieval.
        /// </param>
        /// <param name="datasource">
        /// The name of the datasource being connected to.
        /// </param>
        /// <param name="select">
        /// A SQL statement that retrieves the fields needed for the
        /// report.
        /// </param>
        /// <param name="tablename">
        /// The name of the table.
        /// </param>
        /// <param name="report">
        /// The report the result is for.
        /// </param>
        /// <param name="table">
        /// A reference to the table the plugin is for.
        /// </param>
        /// <returns>
        /// A DataTable containing the data.
        /// </returns>
        DataTable Select(IConnection connection, string datasource,
            string select, string tablename, IReport report,
            Table table);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

### VirtualTablePlugin
The VirtualTablePlugin attribute on the plugin class has the following parameters (see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details on all but the last parameter):

* The ID for the plugin.

* The name of the plugin.

* The type of plugin.

* The name of the virtual table this is a plugin for.

Here's an example:

```csharp
[VirtualTablePlugin("{FC5CDC44-72E7-415F-87F3-CEFB088FF4FE}",
    "SampleVirtualTablePlugin",
    PluginSource.Custom,
    "SampleVirtualTable",
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleVirtualTablePlugin :
    IVirtualTablePlugin
```
