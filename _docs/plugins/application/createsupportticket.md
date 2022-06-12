---
layout: default
title: CreateSupportTicket
nav_order: 4
parent: Application
grand_parent: Plugins
---

When an error occurs in the report writer, you may want to create a support ticket in your support ticket system. Obviously, Horizon Reports doesn't know how to do that, so you can put code in the CreateSupportTicket method of an application plugin to handle that.

## Syntax
```csharp
public object CreateSupportTicket(Exception exception,
    List<string> attachments, string message)
```

## Parameters
*exception*
The exception object with information about the error.

*attachments*
A list of filenames to attach to the ticket. This includes the application log and, if the error occurred when running or designing a report, the SFX file for the report.

*message*
Text the user entered in the error dialog.

## Return value
Anything you want displayed to the user, such as a ticket number, after creating the ticket.
