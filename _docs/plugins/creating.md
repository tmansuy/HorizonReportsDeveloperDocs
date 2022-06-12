---
layout: default
title: Creating Plugin Source Code
nav_order: 1
parent: Plugins
---

The quickest way to get started creating a plugin is to make a clone of the [tnmsoft/horizonreports-project-templates](https://github.com/tnmsoft/horizonreports-project-templates) code repository, and then modify the desired templates. The repository contains example templates for each plugin type, so make sure to remove the templates for plugin types you aren't interested in after cloning. Then:

* Each plugin class has an attribute with information about the plugin. For each plugin to be implemented, replace the placeholder name with an appropriate name, and generate a new GUID for the plugin ID. The *Create GUID* menu item under the tools menu in Visual Studio can be used to generate a new GUID.

* Visit each *// TODO* comment in the plugin template and implement the desired behavior.

Plugin code should be kept in a separate project from function code. After you build the DLL for a plugin project, you need to copy it to the Project_Data\Plugins folder. The DLL for a functions project should be copied to the Project_Data\Functions folder.

If you create a new plugin or function project from scratch, make sure to add the [HorizonReports.Api](https://www.nuget.org/packages/HorizonReports.Api/) nuget package to the project.
