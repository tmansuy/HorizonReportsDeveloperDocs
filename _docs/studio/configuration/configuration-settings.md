---
layout: default
title: Configuration Settings
nav_order: 1
parent: Configuration
grand_parent: Horizon Reports Studio
---

Configuration settings are maintained with the Configuration Settings tab in Studio. To change the value for a setting, select the appropriate category in the Configuration settings tab, and enter the new value for the setting. When finished changing settings, click save.

## Application Settings

* *Support Multi-Languages*: Horizon Reports can support [multiple languages]({% link _docs/studio/multi-language.md %}). However, you may decide to only support a single language. In that case, you don't want the Language option to appear in the Options dialog. Set this to False in this case. You can set the default language using the Default Language setting.

* *Default Language*: This setting specifies what language is used by default. This is useful when you want the initial language used by the report writer to be something other than English, whether or not the Support Multi-Languages setting is set to True. Select the desired language from the drop-down list.

> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> The only languages displayed are the ones for which there are resource files in the Resources folder.

* *Allow Access to Reports When No Access to Fields*: [Role-based security]({% link _docs/studio/security.md %}) in the data dictionary allows you to define which roles have access to certain fields. For example, you may want all users to see most fields in the Employees table but only managers should be able to see the Salary field. In that case, you'd create a role in Studio named Managers and set the Roles property of the Salary field to that role. Users who aren't in the Managers role cannot see the Salary field in the Report Writer, so they cannot include it in a report or filter on it. However, what happens to a report that includes the Salary field that someone in the Managers role created?
Normally, such a report does not appear in the Reports Explorer for users who aren't in the Managers role. That means if you want a report showing employee information, you need two reports: one that includes Salary that Managers can see and one that does not that everyone else can see. What if you want to be able to create only one report which includes Salary but hide that field from non-Manager users?
This setting allows you to do that. With this set to the default of False, only Manager users can see and run the report. Settting this to true allows non-Manager users to see and run the report but the report acts as if the Salary field wasn't added to it; the report runs but does not show the Salary field.
If a non-Manager user edits the report, they get a warning message that the report contains some fields they don't have access to and if they save the report, those fields are lost. To prevent that from happening, you should set the security of the report so Everyone has read-only access to the report and Managers has full access.

* *Send Support Tickets to Support Email Address*: When an error occurs, normally the user is prompted to create a support ticket, although you can specify your own ticketing system using a stting. However, if you have an email address that automatically creates tickets from messages sent to it, set this setting to True. In that case, when an error occurs, an email is sent to the email address specified in the Support Email setting. That way, the ticket is created in your ticketing system so you can respond to the user.
Note that the email credentials used to send the email come from the "Demo Email" settings in Web set of configuration settings, so be sure to fill those in as well.

* *Encrypt Connection Strings*: Studio stores the connection settings for the data dictionary database and the connection settings for the databases used for security, formulas, and tags tables. If you want the connection strings to be stored as encrypted values, set this setting to True.

* *Conn. String for Horizon Reports Query data*: This specifies the connection string for the database used to store security, formulas, and tags. The default is a SQLite database named SQData.dat. 

* *Provider for Horizon Reports Query data*: This setting specifies the data provider to use for this database.

* *Automatically Query Values When Editing Filter*: If this setting is True, the report writer retrieves the unique values for the field in a filter condition as the user enters a value for the condition. Turn this off if this causes performance issues.

## Branding Settings

* *Application Name*: This property is the name shown in various places, such as the home page of the web application and in the About dialog. You can assign a name such as "Report Writer for MyApplication," "MyApplication Query," or "Bob's Report Writer."

* *Short Application Name*: This property is similar to the Application Name property, but is used as an abbreviated name in various places. For example, if you set Application Name to "The Northwind Company Reporting System," you may want to use a shorter name like "Northwind Reporting." Leave this setting blank to use the Application Name property in places where Short Application Name would be used.

* *Company Name*: The Company Name property is the name you want displayed in the About dialog. Set this to your company name to private-label or brand Horizon Reports.

* *Company Web Site*: The Company Web Site property is the Web site you want displayed in the About dialog. You don't have to include "http://;" this is added automatically. Set this to your company's web site URL to private-label or brand Horizon Reports.

* *Company Twitter URL*: The Company Twitter URL property is the Twitter page you want linked to in the About dialog. Set this to your company's Twitter URL to private-label or brand Horizon Reports.

* *Company Facebook URL*: The Company Facebook URL property is the Facebook page you want linked to in the About dialog. Set this to your company's Facebook page URL to private-label or brand Horizon Reports.

* *Sales Email*: If the *Users can register on login page* setting is true, when a user registers an account, an email is sent to the email address specified in Sales email. Set this to your company's sales email address to private-label or brand Horizon Reports.

* *Support Email*: The Support Email property is the email address you want displayed in the About dialog. Set this to your company's support email address to private-label or brand Horizon Reports.

* *URL for Technical Support Site*: If you fill in a URL for the URL for Technical Support Site property, a "Technical Support" function appears in the Help menu in the report writer. When the user selects this function, their browser navigates to the specified URL. This is a convenient way for your user to get to your support web site.

* *URL for End User Documentation*: If you've created a branded version of the end user help files, fill in the URL for the custom help files here. If this setting is left blank, the default URL used for user documentation is https://docs.horizon-reports.com.

* *URL for News*: If you fill in this setting, the About dialog, available from the Help menu, includes a link to navigate the browser to that URL, which is normally the blog for your company but could also be a news or press releases page of your web site.

* *URL for Customer Portal*: If you fill in this setting, the Help menu includes a link to navigate the browser to that URL, which is normally a customer portal of some type.

* *Logo Image File*: The setting is the name of an image file displayed in the Login page of Horizon Reports. Leave this blank to display the Horizon Reports logo, or specify the name of an image file (GIF, JPG, or BMP) to use instead. Although the path for the file is shown as fully qualified, it's actually stored as a relative path from the project directory to prevent file location problems.

* *Icon File*: If you want to use your own icon rather than the Horizon Reports icon (![](/assets/images/favicon.ico)), specify the name of an ICO file for the Icon File property. For the web version, this is used as the icon in the browser.

## Data Settings

* *Allow Multiple Data Sources*: If you want to allow your users to query on different sets of data, set this setting to True. When this setting is True, the Login page displays a drop-down list of data sources defined to Horizon Reports, allowing the user to choose which data source to query on. You can use the [GetDataSources]({% link _docs/plugins/dataengine/getdatasources.md %}) method of a data engine plugin to add the data sources that should be available to the end user.

* *Trailing Spaces Insignificant in Joins*: Normally, trailing spaces in fields are insignificant when doing joins. For example, if the foreign key field in a child table contains "ABC     " (with several spaces at the end) and the primary key field in the parent table contains "ABC" (with no trailing spaces), the join usually works correctly. However, some database engines treat the trailing spaces as significant and the join won't work. In that case, turn this setting to false.

* *Default Table For New Reports*: This property specifies which table is initially selected in the Data Selection step of the report wizards when the user creates a new report. If this setting is empty, the first table in alphabetical order (by caption, not real name) is selected. To change this setting, select the desired table from the drop-down list.

* *Default Data Group for New Reports*: This property specifies which [data group]({% link _docs/studio/datadictionary/table-properties.md %}) is initially selected in Step 1 of the report wizards when the user creates a new report. To change this setting, select the desired data group from the drop-down list.

* *Display 'Source Database' field*: If you set this to false, the 'Source Database' field that normally appears in each table when there's more than one datasource will instead be hidden."),

* *Include Joins in the Where Clause*: Some database engines, such as Microsoft Access or older versions of Oracle, do not work properly with joins between tables specified in a JOIN clause of a SQL statement. Instead, they expect joins to be specified in the WHERE clause. For example, instead of using the following SQL statement for a query joining four tables:

    select Products.ProductName,Customers.CompanyName
      from [Order Details]
        inner join Orders
          on [Order Details].OrderID=Orders.OrderID
        inner join Products
          on [Order Details].ProductID=Products.ProductID
        inner join Customers
          on Orders.CustomerID=Customers.CustomerID

use the following instead:

    select Products.ProductName,Customers.CompanyName
      from Products,[Order Details],Orders,Customers
      where [Order Details].OrderID=Orders.OrderID and
        [Order Details].ProductID=Products.ProductID and
        Orders.CustomerID=Customers.CustomerID

Set this to True if your database engine requires joins specified in this manner.

* *Horizon Reports Performs Joins*: Some database engines, such as Btrieve, older versions of Pervasive, and dBase, do not perform multi-table joins very quickly. If join performance is slow, try changing this to True and Horizon Reports will join tables in memory.

* *Default for auto-adding Distinct*: If you filter on a field from a table that isn't involved in a report, you may end up with duplicate records. For example, say your report displays the Company Name and Contact Name from the Customers table. If you filter on the Product Name from the Products table being "Apricot Jam" (in other words, you want a list of customers who bought that product), you'd end up with each customer showing up once for every order they placed for that product. So, if Sam's Grocery ordered it 25 times, they'd appear on the report 25 times. That isn't typically something you'd want, so the report writer eliminates these duplicate records by automatically adding a DISTINCT clause to the query in that case.

However, there may be times when this isn't the correct behavior. For example, if you want to show fields from the Orders table (Order Date, Product Name, and Quantity Ordered) but filter on Company Name is "Sam's Grocery," the report writer eliminates what it thinks are duplicate records, such as two orders for the same product and same quantity on the same day. Clearly, this isn't correct;you'd end up with some missing data. The *Retrieve distinct records* setting in the report wizards allows you to change that.

In certain types of applications, such as an accounting system, you may want the default behavior to not add the DISTINCT clause under these circumstances (that is, have the *Retrieve distinct records* setting default to Never) and allow the user to turn that setting off for a particular report. This setting controls that default.

* *Display Show All Data Groups Options*: If this setting is set to True, the *Show all data groups* control appears in Step 1 of the report wizards if there are two or more data groups. Change this setting to False to force the user to select a specific data group.

* *How to Filter Unfavored Tables by Default*: This setting specifies how the report writer handles a filter condition on the unfavored table of an outer join by default. 

* *Use "with (nolock)"*: Set this option to True to use the "with (nolock)" hint on all tables. This is ignored unless you're using Microsoft SQL Server.

* *Skip Schema Retrieval when Running a Report*: If you set this option to true, the report writer will skip retrieving the schema for a query prior to actually executing the query. This can slightly improve performance, but database queries issued this way cannot be cancelled.

## Web Settings

* *Users Can Register on Login Page*: If this is set to True, unauthorized users can click a link on the login page to be given access to the application. This is typically only turned on in demo web sites. Note that the link only appears if the various Demo Email settings are filled in.

* *Server Email Sender Address*: This is the email address to send server messages (Password Resets, New User Registration, etc...) from.

* *Server Email Sender Name*: This is the descriptive name of the sender server messages are from.

* *Server Email SMTP Server*: This is the address of the SMTP server to send the messages from.

* *Server Email SMTP Port*: This is the port to use for the SMTP server when sending messages.

* *Server Email SMTP User Name*: This is the user name of the mail account to send server messages from.

* *Server Email SMTP Password*: This is the password of the mail account to send server messages from.

* *Support Multi-Tenant Environment*: Set this setting to True to enable [multi-tenant support]({% link _docs/studio/multi-tenant.md %}).

* *Filter Field for Queries in Multi Tenant Environment*: If all tenants share a database, but each table has a certain field containing an ID indicating which tenant the record belongs to, then use this setting to specify the field.

* *Data Type of Tenant Filter Field*: This specifies the data type of the field specified in the *Filter field for queries in multi-tenant* setting.

* *Disable Slide Toggles*: Set this to true to hide the slide toggle style checkboxes and display standard checkboxes instead.

## Auth Settings

* *Log Off Redirect URL*: The report writer will normally redirect the user to the login page (external or internal) when a user logs off. However if you'd like to override this behavior and redirect to a different URL on log off, specify the URL you'd like to redirect to in this setting.

* *Allow Password Resets*: Set this to true to allow a user to request a password reset email in case they forget their password.

* *ADFS Metadata Address*: The metadata address to use if you're using [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via ADFS.

* *ADFS Realm*: The realm (or WtRealm) address to use if you're using [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via ADFS.

* *OpenID Authority*: The Authority to use if you're using [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via OpenID Connect.

* *OpenID Client ID*: The Client ID to use if you're using [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via OpenID Connect.

* *OpenID Client Secret*: The Client secret to use if you're using [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via OpenID Connect.

* *Facebook App ID*: Set this value to your Facebook app ID if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Facebook.

* *Facebook App Secret*: Set this value to your Facebook app secret if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Facebook.

* *Google Client ID*: Set this value to your Google client ID if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Google.

* *Google Client Secret*: Set this value to your Google client secret if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Google.

* *Twitter Consumer Key*: Set this value to your Twitter consumer key if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Twitter.

* *Twitter Consumer Secret*: Set this value to your Twitter consumer secret if you'd like to use [external authentication]({% link _docs/how-to/externalidentproviders.md %}) via Twitter.

* *Timeout*: This specifies the timeout period in minutes for the current logged in user. If there is no activity for this period of time, the user is automatically logged out. The default is 20.