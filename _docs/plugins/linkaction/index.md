---
layout: default
title: Link Action
nav_order: 8
has_children: true
parent: Plugins
---

Link action plugins allow you to create custom events to be executed when a user clicks a field in a report. For example, you may want to display an address in Google Maps when the user clicks it.

A link action plugin implements the [ILinkActionPlugin](VFPS://Topic/_57M0WSOEO) interface and uses the LinkActionPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### ILinkActionPlugin
Here's the definition of ILinkActionPlugin:

```csharp
using HorizonReports.ReportEngine;
using System;
using System.Collections.Generic;
using System.Data;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Link Action plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an attribute that implements ILinkActionPluginMetaData.
    /// </remarks>
    public interface ILinkActionPlugin : IBasePlugin
    {

        /// <summary>
        /// The descriptive name the end user will see for this link action.
        /// </summary>
        string Caption { get; }

        /// <summary>
        /// This method is called when the corresponding field for this action is clicked.
        /// </summary>
        /// <param name="value">
        /// The value of the clicked field
        /// </param>
        /// <param name="report">
        /// The current report
        /// </param>
        /// <param name="data">
        /// The data table for the current report
        /// </param>
        void PerformLinkAction(object value,
            IReport report, DataTable data);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins]({% link _docs/plugins/index.md %}) topic for information about Application.)

### LinkActionPlugin
The LinkActionPlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins]({% link _docs/plugins/index.md %}) topic for details. Here's an example:

```csharp
[LinkActionPlugin("{5E1C95FD-014F-4F5F-AE1A-F0D5C1E2FA13}",
    "SampleLinkActionPlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleLinkActionPlugin : ILinkActionPlugin
```
