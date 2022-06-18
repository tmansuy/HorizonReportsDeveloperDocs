---
layout: default
title: SaveSettings
nav_order: 2
parent: Setup
grand_parent: Plugins
---

The SaveSettings method allows you to decide how to save the settings, such as in a configuration file or the Windows Registry.

## Syntax
```csharp
public bool SaveSettings(Dictionary<string,
    Dictionary<string, string> settings)
```

## Parameters
*settings*
A list of the settings to save. See [GetSettings]({% link _docs/plugins/setup/getsettings.md %}) for a description.

> @icon-info-circle The dictionary has upper case keys, regardless of what case was originally used.

## Return value
True if it succeeded.
