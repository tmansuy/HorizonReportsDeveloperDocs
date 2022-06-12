---
layout: default
title: GetSettings
nav_order: 1
parent: Setup
grand_parent: Plugins
---

The GetSettings method allows you to define the additional settings used by the plugin.

## Syntax
```csharp
public Dictionary<string, Dictionary<string, string>&gt; GetSettings()
```

## Parameters
None.

## Return value
A list of the settings as a Dictionary<string, Dictionary<string, string>&gt;. The string is the ID for the setting and the Dictionary<string, string> is a dictionary of key-value pairs, where the key is the key of a setting and the value is its current value. The top dictionary only contains multiple entries if the AllowMultiple property is true.
