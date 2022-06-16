---
layout: default
title: Setup
nav_order: 10
has_children: true
parent: Plugins
---

Setup plugins allow you to specify additional settings in the Setup Wizard. The report writer doesn't use these settings, but another of your plugins could, by retrieving the value of the setting and then doing something with it.

A setup plugin implements the *ISetupPlugin* interface and uses the SetupPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### ISetupPlugin
Here's the definition of ISetupPlugin:

```csharp
using System;
using System.Collections.Generic;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Setup plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an attribute
    /// that implements ISetupPluginMetaData.
    /// </remarks>
    public interface ISetupPlugin : IBasePlugin
    {
        /// <summary>
        /// Custom settings appear in tabs in the setup dialog. This
        /// property specifies the caption for the tab.
        /// </summary>
        string Caption { get; }

        /// <summary>
        /// True if this plugin should be active.
        /// </summary>
        bool Enabled { get; }

        /// <summary>
        /// True if we need to get values for these settings from the
        /// user. This is typically true the first time a user launches
        /// the app, but not necessarily.
        /// </summary>
        bool NeedSetup { get; }

        /// <summary>
        /// True if the user can add new items to the items managed
        /// by this plugin.
        /// </summary>
        bool UserCanAddNewItems { get; }

        /// <summary>
        /// True if multiple values are allowed. In that case, a list
        /// is displayed with add and remove buttons.
        /// </summary>
        bool AllowMultiple { get; }

        /// <summary>
        /// A list of the settings.
        /// </summary>
        IEnumerable<ISetupOption> Settings { get; }

        /// <summary>
        /// Validates the settings.
        /// </summary>
        /// <param name="values">
        /// A list of the settings to validate.
        /// </param>
        /// <returns>
        /// True if the values are valid.
        /// </returns>
        bool Validate(Dictionary<string, string> values);

        /// <summary>
        /// Saves the settings to the desired location (configuration
        /// file, Windows Registry, etc.).
        /// </summary>
        /// <param name="settings">
        /// A list of the settings to save. See GetSettings for a
        /// description.
        /// </param>
        /// <returns>
        /// True if it succeeded.
        /// </returns>
        bool SaveSettings(Dictionary<string, Dictionary<string, string>>
            settings);

        /// <summary>
        /// Gets the settings from wherever they're stored (configuration
        /// file, Windows Registry, etc.).
        /// </summary>
        /// <returns>
        /// A list of the settings. The string is the ID for the setting
        /// and the Dictionary<string, string> is a dictionary of
        /// key-value pairs, where the key is the key of a setting and
        /// the value is its current value. The top dictionary only
        /// contains multiple entries if AllowMultiple is true.
        /// </returns>
        Dictionary<string, Dictionary<string, string>> GetSettings();
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins]({% link _docs/plugins/index.md %}) topic for information about Application.)

### SetupPlugin
The SetupPlugin attribute on the plugin class has the following parameters (see the [Plugins]({% link _docs/plugins/index.md %}) topic for details on these parameters):

* The ID for the plugin.

* The name of the plugin.

* The type of plugin.

Here's an example:

```csharp
[SetupPlugin("{CAA60206-589F-4801-80F8-A8D674DBCF27}",
    "SampleSetupPlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleSetupPlugin : ISetupPlugin
```

### Plugin properties
Setup plugins have the following properties:

<table class="detailtable table-striped">
<tr><th>Property</th><th>Type</th><th>Purpose</th>
</tr>
<tr>
<td>AllowMultiple</td>
<td>bool</td>
<td>True if multiple values are allowed. In that case, a list is displayed with add and remove buttons.</td>
</tr>
<tr>
<td>Caption</td>
<td>string</td>
<td>Custom settings appear in tabs in the setup dialog. This property specifies the caption for the tab.</td>
</tr>
<tr>
<td>Enabled</td>
<td>bool</td>
<td>True if this plugin should be active.</td>
</tr>
<tr>
<td>NeedSetup</td>
<td>bool</td>
<td>True if we need to get values for these settings from the user. This is typically true the first time a user launches the app, but not necessarily.</td>
</tr>
<tr>
<td>Settings</td>
<td>IEnumerable&lt;ISetupOption&gt;</td>
<td>A list of the settings.</td>
</tr>
<tr>
<td>UserCanAddNewItems</td>
<td>bool</td>
<td>True if the user can add new items to the items managed by this plugin.</td>
</tr>
</table>
