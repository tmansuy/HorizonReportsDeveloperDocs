---
layout: default
title: Creating Help
nav_order: 1
parent: Deploying Horizon Reports
---

The end user Report Writer has a HTML-based help (similar to this site) that describes all the functionality and provides a "how to" section. By default, the report writer will link to http://docs.horizon-reports.com for help. You can also create a customized help site. This allows you to make changes to the [Application Name]({% link _docs/studio/configuration/configuration-settings.md %}) or other settings. 

## Creating customized help
The default help documentation uses a source repository and [GitHub Pages](https://pages.github.com/). To create customized help for your Horizon Reports project, do the following:

* Fork the [repository](https://github.com/tmansuy/HorizonReportsDocs) for the help. 

* Edit the _config.yml file and update the variables in the *Horizon Reports Documentation Settings* section. See below for a description of the settings to update.

* Finish [creating](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site) your GitHub Pages site.

* Update the *URL for end user help documentation* setting with the URL for your customized help.

## _config.yml Settings

* *title*: The title for the help web site.

* *email*: The contact email address to display in the documentation.

* *app_name*: The application name (e.g. Report Writer) to display in the documentation.

* *has_datagroups*: Set to **true** if you've defined data groups in your project.

* *has_multilanguage*: Set to **true** if you support multiple languages.

* *has_multidatasource*: Set to **true** if the end user can choose from multiple data sources.

* *has_tenants*: Set to **true** if tenant support is enabled for your project.

* *manage_conn_string*: Set to **true** if a database in the project uses the *User can Manage Connection String* setting.

* *manage_dsn*: Set to **true** if a database in the project uses the *User can Manage DSN* setting.

* *users_can_register*: Set to **true** if users can register for new accounts.

* *allow_password_reset*: Set to **true** if users are able to reset their password.

* *support_center*: Set to **true** to display the support center topic.

* *support_center*: Set to **true** to display the knowledge base topic.

* *company*: The company name to display in the documentation.

* *description*: The description of the help repository.

* *url*: the base hostname & protocol for your site, e.g. https://docs.horizon-reports.com

## Further customizing help
You may want to consider customizing the following:

* Add any additional information desired to the Technical Support topic under.

* If you create a [Setup plugin](vfps://Topic/_3QV0S1XDP), add a topic under the Configuration section describing any additional options you defined in the plugin.

Edit the markdown (.md) files for the appropriate help topics using your favorite text editor.