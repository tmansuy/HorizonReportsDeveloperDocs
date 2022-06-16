---
layout: default
title: Custom Output
nav_order: 7
has_children: true
parent: Plugins
---

A Custom Output plugin allows you to specify a custom output type for a schedule. By default, users can email a report or upload it to an FTP site. This plugin allows you to specify a new type, like uploading to Azure, or storing in a local document database, for example.

A Custom Output plugin implements the *ICustomReportOutputPlugin* interface and uses the CustomReportOutputPluginAttribute attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

## ICustomReportOutputPlugin
Here's the definition of ICustomReportOutputPlugin:

```csharp
using HorizonReports.ReportEngine;
using System.IO;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Custom Output type plugins must implement.
    /// </summary>
    public interface ICustomReportOutputPlugin : IBasePlugin
    {

        /// <summary>
        /// The descriptive name the end user will see for this output type
        /// </summary>
        string Caption { get; }

        /// <summary>
        /// Executes after a report is finished. Use this method to perform the output
        /// type (e.g. upload to FTP, save to disk, etc...)
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <param name="reportStream">
        /// The Stream containing the report contents
        /// </param>
        /// <param name="filename">
        /// The name of the file that should be created.
        /// </param>
        bool PerformOutput(IReport report, Stream reportStream, string filename);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

## CustomReportOutputPlugin
The CustomReportOutputPlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details. Here's an example:

```csharp
[CustomReportOutputPlugin("{411833A-CC11-4EAB-96A7-11F7D5405D01}",
        "AzureUpload",
        PluginSource.Custom,
        Version = "1.0.0.0",
        ExecutionPriority = 5)]


    public class CustomAzureOutputPlugin : ICustomReportOutputPlugin
```
