---
layout: default
title: BeforeLoaded
nav_order: 2
parent: Data Dictionary
grand_parent: Plugins
---

The BeforeLoaded method can be used for any tasks necessary before the data dictionary is loaded, such as altering the connection settings for the data dictionary or formulas database.

## Syntax
```csharp
public void BeforeLoaded()
```

## Parameters
None.

## Example
Here's an example that changes the connection settings for the formulas database before loading the data dictionary.

```csharp
using HorizonReports;
using HorizonReports.DataDictionary;
using HorizonReports.Plugins;
using HorizonReports.Storage;
using System.ComponentModel.Composition;
&nbsp;
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
        /// Called before the data dictionary collections are loaded
        /// so we can do anything necessary. In this case, we'll change
        /// the connection string for the formulas database.
        /// </summary>
        public void BeforeLoaded()
        {
            IProvider provider = new Provider(Application.Configuration.Application.FormulasProviderFile);
            provider.SaveConnection(Application.Configuration.Application.FormulasConnectionName,
                "Data Source=MyFormulasDatabase.dat",
                "System.Data.SQLite", false);
        }

        public string GetVersion(IField item)
        {
            return "";
        }

        public string GetVersion(ITable item)
        {
            return "";
        }

        public string GetVersion(IJoin item)
        {
            return "";
        }
    }
}
```
