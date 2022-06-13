---
layout: default
title: PerformAction
nav_order: 1
parent: Web Action
grand_parent: Plugins
---

The PerformAction method is called when the plugin's corresponding URL is navigated to, and the method returns an appropriate HTTP response.

## Syntax
```csharp
public System.Net.Http.HttpResponseMessage PerformAction(string[] actionParams,
    System.Net.Http.HttpRequestMessage request)
```

## Parameters
*actionParams*
A list of the settings to validate.

*request*
The HTTPRequestMessage object.

## Return value
An HttpResponseMessage object to be sent as the response.
