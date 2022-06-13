---
layout: default
title: Web Action
nav_order: 14
has_children: true
parent: Plugins
---

Web action plugins support custom actions in a web browser. The plugin's PerformAction method is called when its corresponding URL is navigated to, and the method returns an appropriate HTTP response.

A web action plugin implements the [IWebActionPlugin](VFPS://Topic/_4KB0ZPIOI) interface and uses the WebActionPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.


### IWebActionPlugin
Here's the definition of IWebActionPlugin:

```csharp
using System;
using System.Collections.Generic;
using System.Net.Http;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Web Action plugins must implement.
    /// </summary>
    /// <remarks>
    /// Plugin classes implementing this interface must have an
    /// attribute that implements
    /// IWebActionPluginMetaData.
    /// </remarks>
    public interface IWebActionPlugin :
        IBasePlugin
    {
        /// <summary>
        /// Performs the custom web action.
        /// </summary>
        /// <param name="values">
        /// A list of the settings to validate.
        /// </param>
        /// <returns>
        /// HttpResponseMessage to be sent as the response.
        /// </returns>
        HttpResponseMessage PerformAction(string[] actionParams,
            HttpRequestMessage request);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

### WebActionPlugin
The WebActionPlugin attribute on the plugin class has the following parameters (see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details on these parameters):

* The ID for the plugin.

* The name of the plugin.

* The type of plugin.

Here's an example:

```csharp
[WebActionPlugin("{FC5CDC44-72E7-415F-87F3-CEFB088FF4FE}",
    "SampleWebActionPlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleWebActionPlugin : IWebActionPlugin
```

