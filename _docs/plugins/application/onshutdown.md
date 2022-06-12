---
layout: default
title: OnShutdown
nav_order: 5
parent: Application
grand_parent: Plugins
---

The report writer calls the OnShutdown method of any Application plugins when the application terminates. This can be used to perform any desired cleanup tasks.

## Syntax
```csharp
public void OnShutdown()
```

## Parameters
None.

