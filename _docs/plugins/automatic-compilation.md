---
layout: default
title: Automatic Compilation
nav_order: 2
parent: Plugins
---

Horizon Reports can automatically compile your plugins or functions for you if they are written in C#. To use this feature, create a subfolder named "Source" in your *Project_Data\Plugins* folder for plugins, or *Project_Data\Functions* for functions. Then, copy each C# source code file (*.cs) to the corresponding "Source" folder.

During application startup, Horizon Reports enumerates the source files (e.g. Project_Data\Plugins\Source\MyPlugin.cs) and looks for a corresponding plugin in the Plugins folder (e.g. Project_Data\Plugins\MyPlugin.dll). If the plugin is not found, then the source file is compiled.

### Dependencies

During compliation, references to most assemblies that are part of .NET 6 are available. However, if your code depends on additional assemblies (for example, from a nuget package), then copy the assembly file (.dll) to the source folder as well.