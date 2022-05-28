---
layout: default
title: Home
nav_order: 1
description: "This is the developer documentation for the ad hoc reporting tool Horizon Reports"
permalink: /
has_children: true
---

![](/assets/images/banner.png)

Horizon Reports is an award-winning, easy-to-use, ad-hoc report writer. It can query against many different sources of data, including:

* Databases such as Microsoft SQL Server, Oracle, PostgreSQL, IBM Db2, and MySQL.

* Microsoft Excel spreadsheets.

## Features

Horizon Reports has a simple "wizard" interface. After selecting a report from the list of available reports, the user can preview the report or output it to one of several types of files (PDF, Microsoft Excel, RTF, etc.).

In addition to running pre-defined reports, they can create their own reports in just minutes. They simply select which fields to report on from the list of available fields (with meaningful descriptive names rather than cryptic names and symbols), and they're done! They don't need detailed knowledge of the database schema and how to join tables; Horizon Reports takes care of that for them.

What makes Horizon Reports easy to use is that it has detailed knowledge about the databases it queries against. This means the user doesn't have to know what a join is, let alone how to create a join for a particular set of tables. They don't have to know the names of tables and fields. They don't have to know how the data is stored. They simply tell Horizon Reports what they want and it figures out how to get the data they need.

## Configurable

What gives Horizon Reports this knowledge about the databases is a set of application-specific configuration settings. These config settings can be broken down into four groups:

* *Data dictionary*: the data dictionary describes what the databases Horizon Reports can access look like: the tables, fields, and relationships between the tables. This information includes the caption for tables and fields, output formatting for fields (such as the format to use for numeric fields and any formulas or functions to use to convert the data from how it's stored to how the user expects to see it), the types of joins between tables (outer or inner), etc.

* *Configuration*: these settings describe how Horizon Reports behaves: what name appears in the title bar of the window, whether multiple data sets are supported or not, and so on.

* *Resources*: you may wish to change the wording that Horizon Reports uses in various dialogs or support multiple languages for field and table captions. Resource files allow you to specify what to display to the user for certain key phrases.

* *Plugins*: using plugins written in any Microsoft .NET language, you can customize the behavior of the report wizards, data retrieval, and report runs. Support for multi-tenant environments is easily implemented using plugins.

A set of application-specific configuration settings is called a "project." Horizon Reports supports multiple projects; for example, you could have versions of Horizon Reports that report on an accounting system, a customer relationship management system, and a warehouse application.