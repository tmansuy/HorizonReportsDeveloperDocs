---
layout: default
title: BeforeLogin
nav_order: 2
parent: Application
grand_parent: Plugins
---

The report writer calls the BeforeLogin method of any application plugin after the user enters their user name and password but just before they're logged in.

## Syntax
```csharp
public bool BeforeLogin(string userName)
```

## Parameters
*userName*
The name of the user logging in.

## Return value
True if the application should continue, False if it should terminate.
