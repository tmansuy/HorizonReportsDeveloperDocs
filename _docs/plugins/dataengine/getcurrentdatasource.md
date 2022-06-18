---
layout: default
title: GetCurrentDataSource
nav_order: 2
parent: Data Engine
grand_parent: Plugins
---

The report writer calls the GetCurrentDataSource method of a data engine plugin to determine which data source to connect to when running a report. This method should only return a data source name if the GetDataSources method defines multiple data sources but the project's [Allow Multiple Data Sources]({% link _docs/studio/configuration/configuration-settings.md %}) setting is false, meaning the user doesn't get to choose which data source they want because the plugin does it for them. In that case, this method should make a decision (likely based on the currently logged in user) about which data source to choose. Under any other conditions, this method should return null.

For example, suppose you're hosting Horizon Reports in a multi-tenant environment where users from different customers can log in. Each customer has their own database (all the databases have the same logical structure matching that defined in the data dictionary) so you want a user to automatically connect to the database for their company. Further suppose that which user connects to which database is defined in an XML file like the following:

    <datasources>
        <datasource>
            <database>Database1</database>
            <users>
                <user>Mark</user>
                <user>Doug</user>
            </users>
        </datasource>
        <datasource>
            <database>Database2</database>
            <users>
                <user>Bob</user>
            </users>
        </datasource>
    </datasources>

The GetDataSources method in the sample code shown below defines the two data sources available and the GetCurrentDataSource method specifies which one the current user connects to.

## Syntax
```csharp
public string GetCurrentDataSources(IDataSourceCollection dataSources)
```

## Parameters
*dataSources*
The data sources collection.

## Return value
Null to respect the user's data source choice in the Login page or the name of a data source to force that data source to be used.

## Example
```csharp
using HorizonReports;
using HorizonReports.ConnectionManagement;
using HorizonReports.Plugins;
using HorizonReports.Security;
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.IO;
using System.Reflection;
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
        /// A cache of which users connect to which database.
        /// </summary>
        private Dictionary<string, string> _userDatabases =
            new Dictionary<string, string>();

        /// <summary>
        /// Fill the data source collection with connection settings
        // for each database specified in Datasources.xml.
        /// </summary>
        /// <param name="dataSources">
        /// The data source collection.
        /// </param>
        /// <returns>
        /// True (assumes we succeeded).
        /// </returns>
        public bool GetDataSources(IDataSourceCollection dataSources)
        {
            // Read in the data source information.
            XmlDocument doc = new XmlDocument();
            doc.Load("Datasources.xml");
            XmlNodeList nodes = doc.SelectNodes("datasources/datasource");

            // Add each database to the data sources collection.
            foreach (XmlNode node in nodes)
            {
                string database = node.SelectSingleNode("database").
                    InnerText;
                IDataSource ds = dataSources.New(database);
                SQOdbcConnectionFactory factory =
                    ds.AddConnection("northwind",
                    ConnectionSource.ODBC) as SQOdbcConnectionFactory;
                factory.Driver = "SQL Server";
                factory.Server = "MyServer";
                factory.Database = database;

                // Add the names of the user who connect to this
                // database to our cache.
                XmlNodeList users = node.SelectNodes("users/user");
                foreach (XmlNode user in users)
                {
                    _userDatabases.Add(user.InnerText, database);
                }
            }

            return true;
        }

        /// <summary>
        /// Returns the name of the current data source used for
        /// reports. In this case find the current user in the cache
        /// and return the name of the data source they connect to.
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
            IUser user = Application.Security.CurrentUser;
            string datasource = "";
            if (user != null)
            {
                datasource = _userDatabases[user.Name];
            }
            return datasource;
        }
    }
}
```
