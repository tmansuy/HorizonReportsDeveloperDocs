---
layout: default
title: Data Dictionary
nav_order: 5
has_children: true
parent: Plugins
---

Data dictionary plugins can be used to customize the data dictionary at runtime, such as programmatically adding custom fields that exist in the end-user's database to your project's data dictionary, or to determine what version the database is so [versioned objects]({% link _docs/studio/datadictionary/versioning.md %}) are used correctly.

A data dictionary plugin implements the *IDataDictionaryPlugin* interface and uses the DataDictionaryPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.


## IDataDictionaryPlugin
Here's the definition of IDataDictionaryPlugin:

```csharp
using System;
using HorizonReports.DataDictionary;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that DataDictionary plugins must implement.
    /// </summary>
    public interface IDataDictionaryPlugin :
        IBasePlugin
    {
        /// <summary>
        /// Called after the data dictionary collections are loaded.
        /// </summary>
        void AfterLoaded();

        /// <summary>
        /// Called before the data dictionary collections are loaded.
        /// </summary>
        void BeforeLoaded();

        /// <summary>
        /// Get the version number for the specified table.
        /// </summary>
        string GetVersion(Table item);

        /// <summary>
        /// Get the version number for the specified field.
        /// </summary>
        string GetVersion(Field item);

        /// <summary>
        /// Get the version number for the specified join.
        /// </summary>
        /// <param name="item"></param>
        /// <returns></returns>
        string GetVersion(Join item);
		
		/// <summary>
        /// A reference to the application's DataDictionary.
        /// </summary>
        IDataDictionary DataDictionary { get; set; }
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins]({% link _docs/plugins/index.md %}) topic for information about Application.)

## DataDictionaryPlugin
The DataDictionaryPlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins]({% link _docs/plugins/index.md %}) topic for details. Here's an example:

```csharp
[DataDictionaryPlugin("{815AB23B-403D-418C-A85D-DE8B3B5595FB}",
    "SampleDataDictionaryPlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleDataDictionaryPlugin :
    IDataDictionaryPlugin

```

## Plugin properties
DataDictionary is a reference to an IDataDictionary object. Although you may think you can access the data dictionary through the DataDictionary member of Application, at the time that BeforeLoaded and AfterLoaded are called, Application.DataDictionary hasn't been set yet and is null. So, to access the data dictionary, use the DataDictionary member of the plugin instead.
