---
layout: default
title: Using Horizon Reports from Other Applications
nav_order: 13
parent: How To
---

Horizon Reports has a rich API that makes it easy to run and even create reports programmatically from other applications. A [sample project]({% link _docs/studio/samples.md %}) in the Samples folder, ReportCreation, shows how to do this. ReportCreation is a C# console project that programmatically creates a report and outputs it to Microsoft Excel. 

To use Horizon Reports from your .NET 6 Application, add the HorizonReports.Api Nuget package to your project.

### Instantiating the Application object
In the following code, the SetupQuery method instantiates the Application object into _app. Change the assignment to the projectFolder variable as necessary.

```csharp
/// <summary>
/// A reference to the Application object.
/// </summary>
private static IHorizonReportsAppService _app;
private static IHost App;

/// <summary>
/// Instantiate the Application object.
/// </summary>
private static void SetupQuery(string[] args)
{
    // Get the paths we need.
    string projectFolder = HorizonReports.Library.StringFunctions.MakeAbsolutePath(Directory.GetCurrentDirectory(),
        @"..\..\..\..\Sample Project");
    string configFile = projectFolder + @"\Project_Data\settings.xml";
    string settingsFile = projectFolder + @"\App_Data\ApplicationSettings.xml";

    // Use a host builder to create the necessary service
    var builder = Host.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((context, config) =>
        {
            config.AddEnvironmentVariables();
            if (args != null)
            {
                config.AddCommandLine(args);
            }
        });

    builder.ConfigureServices((buildercontext, services) =>
    {
        var usercontext = new UserContextSettings();
        services.AddHorizonReports(new string[] { Defaults.ApplicationSettingsParameter + "=" + settingsFile, Defaults.ProjectParameter + "=" + configFile }, usercontext);
    });
    App = builder.Build();
    _app = App.Services.GetService<IHorizonReportsAppService>();
}
```

### Application parameters
There are several parameters you can pass to the Application object when you instantiate it. These parameters specify things such as which folder contains the project files. They are passed as an array of name-value pairs as you can see in the code example above.

* *appsettings*: the path to the App_Data\ApplicationSettings.xml file containing application settings.

* *datasource*: the name of the data source to connect to.

* *password*: the password to use to automatically log a user in. As discussed in the [Using Horizon Reports from Other Web Applications]({% link _docs/how-to/usingfromotherwebapps.md %}) topic, it's better to use a token instead.

* *project*: the path to the Project_Data\Settings.xml file containing project settings.

* *username*: the user name to use to automatically log a user in. As discussed in the [Using Horizon Reports from Other Web Applications]({% link _docs/how-to/usingfromotherwebapps.md %}) topic, it's better to use a token instead.

### Running a report
The ExportToExcel method in the following code outputs the specified report to a Microsoft Excel spreadsheet. Note the "TODO" comment; you have to set the values of any ask-at-runtime filter conditions to appropriate values.

```csharp
/// <summary>
/// Output a report to an Excel file.
/// </summary>
private static void ExportToExcel(IReport report)
{
    // See if the report has any ask-at-runtime conditions. If so, we need
    // to supply values.
    var conditions = report.FilterConditions.Where(f => f.AskAtRuntime);
    if (conditions.Count() > 0)
    {
        foreach (FilterCondition condition in conditions)
        {
            // TODO: put the value to use in the following variable:
            object value = null;
            condition.Values.Clear();
            condition.Values.Add(value);
        }
    }
    // Get the result set for the report, then create the layout and do the export
    // if we succeeded or display a message that it failed.
    if (_app.ReportEngine.RetrieveDataForReport(report))
    {
        ReportResult result = report.CreateLayout();
        if (result == ReportResult.Success)
        {
            report.ExportOptions.Type = FileTypes.XLSX;
            report.ExportOptions.FileName = Environment.GetFolderPath(Environment.SpecialFolder.DesktopDirectory) +
                @"\My Excel File.xlsx";
            report.Export();
            OpenFile(report.ExportOptions.FileName);
        }
        else
        {
            _app.Logger.Error("CreateLayout failed: " + result.ToString());
        }
    }

    // We couldn't create the result set, so display a message accordingly.
    else
    {
        _app.Logger.Error("The data retrieval failed. The error message is:\n\n" +
           _app.ReportEngine.Error);
    }
}
```

### Creating a report
The following code creates a report named "My test report." Note that while this code adds the report to the collection and saves it to an SFX file, there's actually no need to do that if you intend to create the report programmatically each time.

```csharp
/// <summary>
/// Create a report and fill it with the desired fields.
/// </summary>
private static IReport CreateReport()
{
   // Create a quick report and add it to the collection.
   QuickReport report = new QuickReport(_app);
   report.Name = "My test report";
   _app.ReportEngine.Reports.Add(report);
   report.Save();
&nbsp;
   // Add Country and group on it. This is one way to add it:
   // create a QuickReportField, set its Field property, and
   // add it to the report's Field collection.
   QuickReportField groupField = new QuickReportField();
   groupField.Heading = "Country";
   groupField.Field = _app.DataDictionary.Fields["Customers.Country"];
   groupField.Group = 1;
   report.Fields.Add(groupField);
&nbsp;
   // Add City and put in the group header for country. This is
   // another way to add it:  pass the New method of the report's
   // Fields collection a reference to the field.
   QuickReportField field = report.Fields.New(
        _app.DataDictionary.Fields["Customers.City"]);
   field.Heading = "City";
   field.InGroupHeader = groupField;
   report.Fields.Add(field);
&nbsp;
   // Add CompanyName.
   QuickReportField company = new QuickReportField();
   company.Heading = "Company";
   company.Field = _app.DataDictionary.Fields["Customers.CompanyName"];
   report.Fields.Add(company);
&nbsp;
   // Add ContactName and right-justify it.
   QuickReportField contactField = new QuickReportField();
   contactField.Heading = "Contact";
   contactField.Field = _app.DataDictionary.Fields["Customers.ContactName"];
   contactField.HorizontalAlignment =
        ReportEngine.TextAlignment.Right;
   report.Fields.Add(contactField);
&nbsp;
   // Add ContactTitle below ContactName.
   field = report.Fields.New(_app.DataDictionary.Fields["Customers.ContactTitle"]);
   field.Heading = "Title";
   field.HorizontalPosition = contactField;
   field.VerticalPosition = 1;
&nbsp;
   // Add Address and Phone.
   field = report.Fields.New(_app.DataDictionary.Fields["Customers.Address"]);
   field.Heading = "Address";
   field = report.Fields.New(_app.DataDictionary.Fields["Customers.Phone"]);
   field.Heading = "Phone";
&nbsp;
   // Filter on Country = "Germany" and ContactTitle = "Sales"
   IFilterCondition filtCondition = report.FilterConditions.New(
        _app.DataDictionary.Fields["Customers.Country"]);
   filtCondition.Values.Add("Germany");
   filtCondition = report.FilterConditions.New(
        _app.DataDictionary.Fields["Customers.ContactTitle"]);
   filtCondition.Connection = new Filtering.AndConnection();
   filtCondition.Values.Add("Sales Representative");
&nbsp;
   return report;
}
```