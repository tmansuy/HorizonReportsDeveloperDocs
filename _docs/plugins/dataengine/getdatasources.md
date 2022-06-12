---
layout: default
title: GetDataSources
nav_order: 1
parent: Data Engine
grand_parent: Plugins
---

As the report writer starts up, each database defined in the data dictionary is given an opportunity to determine which sets of data (data sources) are available. You can customize the behavior of this step by creating a data engine plugin with a GetDataSources method.

The general task to perform in GetDataSources is to add IDataSource objects to the DataSources collection passed to the method and add connections to each one for each database in the data dictionary. The connection settings can be hard-coded, as shown in the first example below, but more likely you'll read it from somewhere, such as a configuration file, as shown in the second example.

It gets a little complex when you have multiple databases in the data dictionary. You must define connection settings for each database in each data source. The second example shows how to do that.

## Syntax
```csharp
public bool GetDataSources(IDataSourceCollection dataSources)
```

## Parameters
*dataSources*
The data sources collection.

## Return value
True if the set of data sources was successfully created.

## Example
This code, taken from SampleDataEnginePlugin.cs in the Samples\SamplePlugins\SamplePlugins folder, creates two data sources for the sample project, one that connects to the Microsoft Access Northwind database in the Sample Project folder and the other to a Microsoft SQL Server database named Northwind.

```csharp
using HorizonReports;
using HorizonReport.ConnectionManagement;
using HorizonReports.Plugins;
using System.ComponentModel.Composition;
using System.IO;
using System.Reflection;

namespace SamplePlugins
{
    [DataEnginePlugin("{FB22E1B5-9AA1-4CE1-9D16-AEFDF0FB6E6C}",
        "SampleDataEnginePlugin",
        PluginSource.Custom,
        Version = "1.0.0.0",
        ExecutionPriority = 5)]
    public class SampleDataEnginePlugin :
        IDataEnginePlugin
    {
        /// <summary>
        /// A reference to the Application object.
        /// </summary>
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        /// <summary>
        /// Create two data sources for the Northwind database: a
        /// Microsoft Access one in the Sample Project folder and a
        /// SQL Server one.
        /// </summary>
        /// <param name="dataSources">
        /// The data source collection.
        /// </param>
        /// <returns>
        /// True (assumes we succeeded).
        /// </returns>
        public bool GetDataSources(IDataSourceCollection dataSources)
        {
            // Remove the default data source used by
            // Studio. This is only  needed if the database's
            // ConnectionType property is set to UseDefaultConnection.

            if (dataSources.Count > 0)
            {
                Application.Logger.Info("Removing default database");
                dataSources.RemoveAt(0);
            }

            // Create the Microsoft Access data source; we'll specify
            // the connection string.
            string databasePath = Path.GetDirectoryName(
                Application.Configuration.Project.ProjectFile) +
                @"\northwind.mdb";
            _logger.InfoFormat("Adding Access database: {0}",
                databasePath);
            IDataSource ds = dataSources.New("Northwind Access");
            ds.Description = "Northwind Access";
            SQOdbcConnectionFactory factory =
                ds.AddConnection("northwind", ConnectionSource.ODBC)
                as SQOdbcConnectionFactory;
            factory.ConnectionString = @"driver=Microsoft Access " +
                "Driver (*.mdb);dbq=" + databasePath;

            // Create the SQL Server data source; we'll specify the
            // individual components of the connection. Note: change
            // these settings as necessary.
            _logger.Info("Adding SQL Server database");
            ds = dataSources.New("Northwind SQL");
            ds.Description = "Northwind SQL";
            factory = ds.AddConnection("northwind",
                ConnectionSource.ODBC) as SQOdbcConnectionFactory;
            factory.Driver = "SQL Server Native Client 11.0";
            factory.Server = @"(localdb)\v11.0";
            factory.Specifier = "database";
            factory.Database = "northwind";

            return true;
        }

        /// <summary>
        /// Returns the name of the current data source used for
        /// reports. In this case we're returning null meaning use
        /// the data source selected by the user in the login page.
        /// </summary>
        /// <param name="dataSources">
        /// The data source collection.
        /// </param>
        /// <returns>
        /// Null.
        /// </returns>
        public string GetCurrentDataSource(IDataSourceCollection dataSources)
        {
            return null;
        }
    }
}
```

**Example**
Suppose your application uses two databases for each company. In the data dictionary, you call those databases "first" and "second" (these are the logical database names). You have two companies: ABC Software and XYZ Industries. The two physical databases for ABC Software are named "ABC1" and "ABC2," while the two for XYZ Industries are named "XYZ1" and "XYZ2." All databases are on the MyServer server.

The code below creates two data sources, one for each company, each of which has connection settings for the two databases. It reads the connection settings from a configuration file named Datasources.xml. Here's what that file looks like:

    <?xml version="1.0" encoding="utf-8" ?>
    <datasources>
        <datasource name="Company1" description="ABC Software">
            <databases>
                <database name="first" connection="server=MyServer;database=ABC1"/>
                <database name="second" connection="server=MyServer;database=ABC2"/>
            </databases>
        </datasource>
        <datasource name="Company2" description="XYZ Industries">
            <databases>
                <database name="first" connection="server=MyServer;database=XYZ1"/>
              <database name="second" connection="server=MyServer;database=XYZ2"/>
            </databases>
        </datasource>
    </datasources>

Here's the plugin code:

```csharp
using System;
using HorizonReports;
using HorizonReports.ConnectionManagement;
using HorizonReports.Plugins;
using System.ComponentModel.Composition;
using System.Xml;

namespace SamplePlugins
{
    [DataEnginePlugin("{FB22E1B5-9AA1-4CE1-9D16-AEFDF0FB6E6C}",
        "SampleDataEnginePlugin",
        PluginSource.Custom,
        Version = "1.0.0.0",
        ExecutionPriority = 5)]
    public class SampleDataEnginePlugin :
        IDataEnginePlugin
    {
        /// <summary>
        /// A reference to the Application object.
        /// </summary>
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        /// <summary>
        /// Create the data sources defined in Datasources.xml.
        /// </summary>
        /// <param name="dataSources">
        /// The data source collection.
        /// </param>
        /// <returns>
        /// True (assumes we succeeded).
        /// </returns>
        public bool GetDataSources(IDataSourceCollection dataSources)
        {
            // Get a logging object and log the start of the process.
            
            Application.Logger.InfoFormat("Start GetDataSources: {0}",
                DateTime.Now);

            // Load Datasources.xml.
            XmlDocument doc = new XmlDocument();
            doc.Load("Datasources.xml");

            // Process each data source.
            XmlNodeList nodes =
                doc.SelectNodes("/datasources/datasource");
            foreach (XmlNode node in nodes)
            {
                // Get the name and description for the data source.
                string name = node.Attributes["name"].Value;
                string description = node.Attributes["description"].
                    Value;
                Application.Logger.InfoFormat("New datasource: {0}: {1}",
                    name, description);
                IDataSource ds = dataSources.New(name);
                ds.Description = description;

                // Add a connection for each database.
                XmlNodeList databases =
                    node.SelectNodes("databases/database");
                foreach (XmlNode database in databases)
                {
                    string dbName = database.Attributes["name"].Value;
                    string conn = database.Attributes["connection"].Value;
                    Application.Logger.InfoFormat("Adding connection for {0}",
                        dbName);
                    SQSqlClientConnectionFactory factory =
                        ds.AddConnection(dbName,
                        ConnectionSource.SqlServer)
                        as SQSqlClientConnectionFactory;
                    factory.ConnectionString = conn;
                }
            }
            Application.Logger.InfoFormat("Finished GetDataSources: {0}",
                DateTime.Now);

            return true;
        }

        /// <summary>
        /// Returns the name of the current data source used for
        /// reports. In this case we're returning null meaning use
        /// the data source selected by the user in the login page.
        /// </summary>
        /// <param name="dataSources">
        /// The data source collection.
        /// </param>
        /// <returns>
        /// Null.
        /// </returns>
        public string GetCurrentDataSource(IDataSourceCollection
            dataSources)
        {
            return null;
        }
    }
}

```
