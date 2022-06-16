---
layout: default
title: Plugins
nav_order: 4
has_children: true
---

Data dictionary properties and configuration settings can only take Horizon Reports so far. For some things, you need to customize how the report writer behaves. You can do that with plugins. Some examples of where plugins are useful are:

* *Dynamically updating the data dictionary*. For example, your application may allow the user to change the caption for some fields. You probably want the user to see the same captions in the report writer; otherwise, the user might have trouble finding the field they want. In the AfterLoaded method of a data dictionary plugin, which is called just after Horizon Reports fills the data dictionary collection from the data dictionary database, you can change the caption (or any other property) of any field. You can even add or remove fields.

* *Defining data sources*. If the [*Connection type*](vfps://Topic/_0PR0V3L9G) property of a database is set to *Scripted*, a plugin specifies the connection information for the database. You can define multiple data sources for a database if desired.

* *Calling stored procedures*. For a variety of reasons (security, performance, or because the DBA says so), you may want to access the data in a table via a stored procedure rather than by a SQL statement. Since Horizon Reports doesn't know the name of the stored procedure to call or the parameters to pass to it, you have to put code in the [Select](vfps://Topic/_3QV0W6BRP) method of a plugin for the table.

* *Calculated fields*. You may have a [calculated field](vfps://Topic/_0U10UENKF) for which a simple expression won't suffice. For example, suppose the commission for a sale is set to a sliding scale, so higher sales amounts receive a higher commission percentage. In this case, you may have to use a control structure such as a switch statement to determine the amount. The code for this goes into a function plugin called from the [Expression](vfps://Topic/_0OY0TQXLS) property of the field.

There are several different types of plugins in Stonefield Query:

* [Application](vfps://Topic/_0SK0XF365): these plugins are called from various places in the report writer. For example, after Horizon Reports has finished its startup task, the AfterSetup method of an application plugin is called.

* [Data dictionary](vfps://Topic/_3QV0S4C5Y): these plugins are called during specific data dictionary events, such as after the collections have been loaded from the data dictionary database.

* [Data engine](vfps://Topic/_0SK0XH4QO): these plugins are called from various places during data engine processing. For example, the GetDataSources method of such a plugin can programmatically define the data sources (physical connection information) for a database.

* [Functions]({% link _docs/plugins/functions.md %}): these simple plugins provide methods called from various places in Horizon Reports, such as the Expression or Caption properties of a field.

* [Report engine](vfps://Topic/_3X70PTD6Y): these plugins are called from various places during report engine processing, such as determining whether the current user can access a specific report.

* [Setup]({% link _docs/plugins/setup/index.md %}): setup plugins allow you to define additional settings that appear in the Horizon Reports Setup Wizard.

* [Value converter](vfps://Topic/_3QW0PG1T9): these plugins convert a value stored in a field into the value you want displayed to the user. For example, some applications store dates as numeric values, so January 13, 2013 is stored as 20130113. A value converter converts the numeric value to a date value for display in a report, and a date value used as a filter into a numeric value that can be used in the WHERE clause of a SQL statement.

* [Values method](vfps://Topic/_3QW0STVGI): these plugins allow you to programmatically define how to display a list of distinct values for a field rather than having Horizon Reports issue a SELECT DISTINCT SQL statement when the user clicks the Values button.

* [Virtual table](vfps://Topic/_3QV0SA9WN): these plugins return a DataTable to Horizon Reports when the user reports on a virtual table.

<%-- * [Web action](vfps://Topic/_4HB0YOSS0): these plugins support custom actions. The plugin's PerformAction method is called when its corresponding URL is navigated to, and the method is responsible for returning an appropriate HTTP response. %>

Horizon Reports supports any .NET language for a plugin, and targets .NET 6.  When creating a new plugin project, you should create a class library that targets net6.0.

A plugin is identified by Horizon Reports by the following:

* Its assembly is in one of the folders Horizon Reports looks in for plugins:

    * The Plugins subdirectory of the program folder. This is intended for plugins provided by TNM Software, or plugins you create that are common to multiple projects. This folder includes the HorizonReports.Plugins.dll plugin, which handles support ticket creation, features for the Setup dialog, and some built-in value converters.

    * The Plugins subdirectory of the Project_Data folder. This is intended for custom plugins you create that are specific to the project.

    * The Functions subdirectory of the Project_Data folder. This is intended for custom plugins you create that provide functions specific to the project.

* It implements the appropriate Horizon Reports plugin interface and has an attribute providing metadata about the plugin. See the help topic for each plugin type for the interface and attribute to use.

All plugin interfaces derived from a common one, [IBasePlugin](VFPS://Topic/_42110PV9P):

```csharp
using System;
using System.ComponentModel.Composition;
&nbsp;
namespace HorizonReports.Plugins
{
    /// <summary>
    /// All the specific plugin types must extend this interface.
    /// </summary>
    public interface IBasePlugin
    {
		[Import]
        IHorizonReportsAppService Application
        {
            get;
            set;
        }
    }
}
```

Application is a reference to the Horizon Reports Application object, which means you have access the report writer services from your plugin.

> @icon-info-circle In a plugin class, you have to use the [Import] attribute on the Application member to ensure its value is set by our dependency injection framework. For example:
```csharp
[Import]
public IHorizonReportsAppService Application { get; set; }
```

> @icon-info-circle Application is null in the constructor of the plugin, so your code can't use it in that method or any methods called from the constructor.

The plugin attributes have members in common:

* The ID for the plugin. This is normally a GUID as a string, so the easiest way to provide its value is to use the Create GUID function in the Tools menu of Visual Studio.

* The name of the plugin. This is normally the same as the class name but could be different if desired.

* The type of plugin. This should be PluginSource.Custom.

* The plugin version number as a string.

* The execution priority as an integer. This is used to determine the order of execution if there's more than one plugin of a certain type. The higher the number, the earlier the execution.

The sections under this topic describe how the different types of plugins work and how to create them, and gives examples of plugins you may wish to use.

## Plugin code
Plugin code must be thread-safe. The reason is that the report writer may spin up multiple threads when retrieving data for a report, and those threads may end up calling one or more plugins. A few general rules of thumb are to try to reference only local variables when possible, avoid using static fields or properties, and use locks to access resources that may be modified in another thread.
