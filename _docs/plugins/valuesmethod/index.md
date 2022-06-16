---
layout: default
title: Values Method
nav_order: 12
has_children: true
parent: Plugins
---

The usual mechanism for retrieving the values for a field in the report writer is to use a SELECT DISTINCT SQL statement. However, you can use a values method plugin to override this behavior for specific fields. This can be useful if the normal SELECT DISTINCT behavior isn't desirable (for example, if the underlying table is very large).

A values method plugin implements the *IValuesMethodPlugin* interface and uses the ValuesMethodPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### IValuesMethodPlugin
Here's the definition of IValuesMethodPlugin:

```csharp
using System;
using System.Collections;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that ValuesMethod plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an attribute that implements IValuesMethodPluginMetaData.
    /// </remarks>
    public interface IValuesMethodPlugin : IBasePlugin
    {
        /// <summary>
        /// Returns the list of values for the field.
        /// </summary>
        /// <returns>
        /// The list of values for the field.
        /// </returns>
        IList GetValues();
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

### ValuesMethodPlugin
The ValuesMethodPlugin attribute on the plugin class has the following parameters (see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details on all but the last parameter):

* The ID for the plugin.

* The name of the plugin.

* The type of plugin.

* The ID (as a string) of the field associated with the plugin.

Here's an example:

```csharp
[ValuesMethodPlugin("{AD7C8C4D-72E7-415F-87F3-CEFB088FF4FE}",
    "SampleValuesMethodPlugin",
    PluginSource.Custom,
    "ABFFF61B-4E9A-4CAA-87CA-A9279579962C",
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleValuesMethodPlugin :
    IValuesMethodPlugin
```
