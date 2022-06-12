---
layout: default
title: PerformOutput
nav_order: 2
parent: Custom Output
grand_parent: Plugins
---

The PerformOutput method performs the steps necessary to output the report file if the user chose this plugin for output.

## Syntax
```csharp
public bool PerformOutput(IReport report, Stream reportStream, string filename)
```

## Parameters
*report*
The current report object being output.

*reportStream*
The stream containing the report contents.

*filename*
The name of the file the user chose to create.

## Return value
A boolean indicating success or failure.
