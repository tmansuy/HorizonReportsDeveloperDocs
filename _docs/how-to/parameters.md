---
layout: default
title: Adding Parameters to a Report Layout
nav_order: 2
parent: How To
---

You may wish to add parameters to a report layout that control how the report runs. Do the following:

* Edit the report using the Advanced Report Designer.

* In the Report Explorer panel, select the Field List tab. Scroll to the Parameters section and expand it.

* Right click and choose Add Parameter. Enter a name and the appropriate data type.

* Add a label to the layout and bind it to the parameter you created.

* Create a [report engine plugin]({% link _docs/plugins/reportengine/index.md %}).

* Add a reference to DevExpress.XtraReports.v21.2.dll, DevExpress.Printing.v21.2.Core.dll, and DevExpress.Data.v21.2.dll.

* Use code similar to the following in the *AfterCreateLayout* method to set the value of the parameter:

```csharp
DevExpress.XtraReports.UI.XtraReport xreport = (report.Layout as XtraReport);
DevExpress.XtraReports.Parameters.Parameter myparam =
    xreport.Parameters["ParameterName"];
myparam.Value = "My parameter value";
```

where *ParameterName* is the name of the parameter you created in the report.