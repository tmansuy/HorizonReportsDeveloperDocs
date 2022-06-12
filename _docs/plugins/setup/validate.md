---
layout: default
title: Validate
nav_order: 3
parent: Setup
grand_parent: Plugins
---

You can validate the values the user enters in your custom settings with the Validate method.

## Syntax
```csharp
public bool Validate(Dictionary<string, string> values)
```

## Parameters
*values*
A list of the settings to validate.

> @icon-info-circle The dictionary has upper case keys, regardless of what case was originally used.

## Return value
True if the values are valid.
