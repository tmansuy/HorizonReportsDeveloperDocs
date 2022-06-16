---
layout: default
title: Report Engine
nav_order: 9
has_children: true
parent: Plugins
---

Report engine plugins have a couple of purposes: providing an additional layer of security or report control by allowing you to programmatically determine which users can access which reports, and altering a report run, such as changing data retrieval or the report layout.

A report engine plugin implements the *IReportEnginePlugin* interface and uses the ReportEnginePlugin attribute. Your plugin needs references to the HorizonReports.Api and System.ComponentModel.Composition Nuget packages.

### IReportEnginePlugin
Here's the definition of IReportEnginePlugin:

```csharp
using HorizonReports.DataEngine;
using HorizonReports.ReportEngine;
using System;
using System.Data;
using System.IO;

namespace HorizonReports.Plugins
{
    /// <summary>
    /// The interface that ReportEngine plugins must implement.
    /// </summary>
    public interface IReportEnginePlugin : IBasePlugin
    {
        /// <summary>
        /// Returns true if the user can access the specified report.
        /// </summary>
        /// <param name="report">
        /// The report to check.
        /// </param>
        /// <returns>
        /// True if the user can access the specified report.
        /// </returns>
        bool CanUserAccessReport(IReport report);

        /// <summary>
        /// Executes just before the layout for the specified report
        /// is created.
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <returns>
        /// True if the layout process can continue, false if not.
        /// </returns>
        bool BeforeCreateLayout(IReport report);

        /// <summary>
        /// Executes just after the layout for the specified report
        /// is created.
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <returns>
        /// True if the report run can continue, false if not.
        /// </returns>
        bool AfterCreateLayout(IReport report);

        /// <summary>
        /// Executes after the SQL statement has been generated and
        /// is about to be sent to the database engine.
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <param name="sqlStatement">
        /// The SQL statement being used.
        /// </param>
        /// <param name="parameters">
        /// An array of parameters used by the SQL statement.
        /// </param>
        /// <param name="tablename">
        /// The name of the data table being created.
        /// </param>
        /// <param name="conn">
        /// The connection object being used.
        /// </param>
        /// <param name="cmd">
        /// The command object being used.
        /// </param>
        /// <param name="dataSourceName">
        /// The name of the current data source being queried.
        /// </param>
        /// <returns>
        /// The SQL statement to be used or null if the SQL
        /// statement should not be sent to the database.
        /// </returns>
        string AfterSQLStatementGenerated(IReport report,
            string sqlStatement, object[] parameters,
            string tablename, IDbConnection conn,
            IDbCommand cmd, string datasourcename);

        /// <summary>
        /// Executes just before the data for the specified report
        /// is retrieved.
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <param name="dataEngine">
        /// The data engine being used to retrieve the data.
        /// </param>
        /// <returns>
        /// True if the report run can continue, false if not.
        /// </returns>
        bool BeforeDataRetrieved(IReport report,
            IDataEngine dataEngine);

        /// <summary>
        /// Executes just after the data for the specified report
        /// is retrieved.
        /// </summary>
        /// <param name="report">
        /// The report being run.
        /// </param>
        /// <param name="dataEngine">
        /// The data engine being used to retrieve the data.
        /// </param>
        /// <returns>
        /// True if the report run can continue, false if not.
        /// </returns>
        /// <remarks>
        /// The ResultSet property of the report contains the
        /// DataTable used for the report.
        /// </remarks>
        bool AfterDataRetrieved(IReport report,
            IDataEngine dataEngine);

        /// <summary>
        /// Executes after the connnection to the database has been
        /// opened but before the SQL statement is sent to the
        /// database. This can be used to configure the connection,
        /// such as issuing SET ANSI_PADDING OFF or other types of
        /// connection settings.
        /// </summary>
        /// <param name="conn">
        /// The connection object being used; the connection has
        /// been opened.
        /// </param>
        void BeforeSQLStatementSentToDatabase(IDbConnection conn);

        /// <summary>
        /// Executes just before the specified report is saved.
        /// </summary>
        /// <param name="report">
        /// The report being saved.
        /// </param>
        void BeforeReportSaved(IReport report);

        /// <summary>
        /// Executes just after the specified report is saved.
        /// </summary>
        /// <param name="report">
        /// The report being saved.
        /// </param>
        void AfterReportSaved(IReport report);

        /// <summary>
        /// Executes just before the specified report is exported
        /// to a file.
        /// </summary>
        /// <param name="report">
        /// The report being exported.
        /// </param>
        /// <param name="fileName">
        /// The name of the file.
        /// </param>
        /// <returns>
        /// True if the report should be exported, false if not.
        /// </returns>
        bool BeforeExportReport(IReport report, string fileName);

        /// <summary>
        /// Executes just before the specified report is exported
        /// to a stream.
        /// </summary>
        /// <param name="report">
        /// The report being exported.
        /// </param>
        /// <param name="stream">
        /// The stream.
        /// </param>
        /// <returns>
        /// True if the report should be exported, false if not.
        /// </returns>
        bool BeforeExportReport(IReport report, Stream stream);

        /// <summary>
        /// Executes just before the specified report is deleted.
        /// </summary>
        /// <param name="report">
        /// The report being deleted.
        /// </param>
        /// <returns>
        /// True if the report should be deleted, false if not.
        /// </returns>
        bool BeforeReportDeleted(IReport report);

        /// <summary>
        /// Executes just after the specified report is deleted.
        /// </summary>
        /// <param name="report">
        /// The report being deleted.
        /// </param>
        /// <param name="reportWasDeleted">
        /// True if the report was deleted.
        /// </param>
        void AfterReportDeleted(IReport report, bool reportWasDeleted);

        /// <summary>
        /// Executes just before the specified report is copied.
        /// </summary>
        /// <param name="report">
        /// The report being copied.
        /// </param>
        /// <param name="name">
        /// The name to assign to the copy.
        /// </param>
        /// <returns>
        /// True if the report should be copied, false if not.
        /// </returns>
        bool BeforeReportCopied(IReport report, string name);

        /// <summary>
        /// Executes just after the specified report is copied.
        /// </summary>
        /// <param name="report">
        /// The report being copied.
        /// </param>
        /// <param name="copy">
        /// The copied report.
        /// </param>
        void AfterReportCopied(IReport report, IReport copy);

        /// <summary>
        /// Executes when a report is created.
        /// </summary>
        /// <param name="report">
        /// The new report.
        /// </param>
        void ReportCreated(IReport report);
    }
}
```

(As with all plugins that derive from IBasePlugin, it also has an Application member; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for information about Application.)

### ReportEnginePlugin
The ReportEnginePlugin attribute on the plugin class has the usual set of parameters all plugin attributes do; see the [Plugins](vfps://Topic/_0OV0T6LZO) topic for details. Here's an example:

```csharp
[ReportEnginePlugin("{5E1C95FD-014F-4F5F-AE1A-F0D5C1E2FA13}",
    "SampleReportEnginePlugin",
    PluginSource.Custom,
    Version = "1.0.0.0",
    ExecutionPriority = 5)]
public class SampleReportEnginePlugin : IReportEnginePlugin
```
