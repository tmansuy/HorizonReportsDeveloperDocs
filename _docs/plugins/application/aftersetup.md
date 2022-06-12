---
layout: default
title: AfterSetup
nav_order: 3
parent: Application
grand_parent: Plugins
---

The report writer calls the AfterSetup method of any application plugin after all setup tasks are done but before the user is asked to log in.

## Syntax
```csharp
public bool AfterSetup()
```

## Parameters
None.

## Return value
True if the application should continue, False if it should terminate.

## Example
If "user" and "password" parameters are specified on the command line, such as:

    C:\HRWeb\HRWeb.exe
        "project=C:\My Application\Project_Data\settings.xml"
        "appdata=C:\My Application\App_Data\applicationsettings.xml"
        user=etaylor password=diamond

the following code automatically logs in the user specified.

```csharp
using System;
using HorizonReports;
using HorizonReports.Plugins;
using System.IO;
using Stonefield.Library;
using Microsoft.Win32;
using System.ComponentModel.Composition;
using System.Net;
using System.Collections.Specialized;
using System.Text;
using System.Collections.Generic;
&nbsp;
namespace SamplePlugins
{
    /// <summary>
    /// This sample shows how an application plugin might work.
    /// </summary>
    [ApplicationPlugin("{FAFB8ADD-6D11-42B2-B4BF-ADCE6FE0895B}",
        "SampleApplicationPlugin",
        PluginSource.Custom,
        Version = "1.0.0.0",
        ExecutionPriority = 5)]
    public class SampleApplicationPlugin :
        IApplicationPlugin
    {
        /// <summary>
        /// A reference to the Application object.
        /// It must be marked as [Import] so it's automatically set
        /// to the correct object.
        /// </summary>
        [Import]
        public IHorizonReportsAppService Application { get; set; }

        /// <summary>
        /// Fired after the application object setup tasks are done.
        /// This example automatically logs in the user specified on
        /// the command line in the "user" and "password" parameters.
        /// </summary>
        /// <returns>
        /// True if the application can start, false if not. We'll
        /// return true in this case regardless of whether the login
        /// took place or succeeded; if neither, the normal login can
        /// take place.
        /// </returns>
        public bool AfterSetup()
        {
            string user = "";
            string password = "";
            foreach (string parameter in Application.Parameters)
            {
                if (parameter.ToLower().StartsWith("user="))
                {
                    user = parameter.Substring(5);
                }
                else if (parameter.ToLower().StartsWith("password="))
                {
                    password = parameter.Substring(9);
                }
            }
            if (!String.IsNullOrWhiteSpace(user) &&
                !String.IsNullOrWhiteSpace(password))
            {
                Application.Security.Login(user, password);
            }
            return true;
        }
&nbsp;
        /// <summary>
        /// Fired when Stonefield Query shuts down.
        /// </summary>
        public void OnShutdown()
        {
        }
&nbsp;
        /// <summary>
        /// For future use.
        /// </summary>
        public object CreateSupportTicket(Exception exception,
            List<string> attachments, string message)
        {
            return null;
        }
    }
}
```
