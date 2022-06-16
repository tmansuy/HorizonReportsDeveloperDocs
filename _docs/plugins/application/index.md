---
layout: default
title: Application
nav_order: 4
has_children: true
parent: Plugins
---

Application plugins allow you to perform customization tasks at certain application-level events.

An application plugin implements the *IApplicationPlugin* interface and uses the ApplicationPlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

## IApplicationPlugin
Here's the definition of IApplicationPlugin:

```csharp
using HorizonReports.Security;
using System;
using System.Collections.Generic;
using System.Diagnostics.Contracts;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that Application plugins must implement.
    /// </summary>
    public interface IApplicationPlugin : IBasePlugin
    {
        /// <summary>
        /// Called after setup tasks are done.
        /// </summary>
        /// <returns>
        /// True if the application can continue.
        /// </returns>
        bool AfterSetup();

        /// <summary>
        /// Called before the user has logged in.
        /// </summary>
        /// <param name="userName">
        /// The name of the user logging in.
        /// </param>
        /// <returns>
        /// True if the application can continue.
        /// </returns>
        bool BeforeLogin(string userName);

        /// <summary>
        /// Called after the user has logged in.
        /// </summary>
        /// <param name="user">
        /// A reference to the logged-in user.
        /// </param>
        /// <returns>
        /// True if the application can continue.
        /// </returns>
        bool AfterLogin(IUser user);

        /// <summary>
        /// Called when the application is shutting down.
        /// </summary>
        void OnShutdown();

        /// <summary>
        /// Called when a support ticket should be created because
        /// of an exception.
        /// </summary>
        /// <param name="exception">
        /// The exception that occurred.
        /// </param>
        /// <param name="attachments">
        /// A list of attachments for the ticket.
        /// </param>
        /// <param name="message">
        /// The message for the ticket.
        /// </param>
        /// <returns>
        /// Anything the plugin code wants to return to the caller.
        /// </returns>
        object CreateSupportTicket(Exception exception,
            List<string> attachments, string message);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

## ApplicationPlugin
The ApplicationPlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details. Here's an example:

```csharp
[ApplicationPlugin("{9857FB9C-2BA2-46A5-8F8F-60D33B6ABE33}",
    "SampleApplicationPlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleApplicationPlugin : IApplicationPlugin
```
