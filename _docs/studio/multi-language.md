---
layout: default
title: Multi-Language Support
nav_order: 11
parent: Horizon Reports Studio
---

Every dialog caption and message displayed to the user in the report writer is defined in one or more resource files. There are two types of resource files: application and project. Application resource files are located in the Resources subdirectory of the installation program folder. Project resource files are located on the Project_Data folder for the project.

A resource file is an XML file with resource elements providing key-value pairs. The key is used to locate a particular resource and the value is the string to display to the user. Here's an example, taken from resources.en.xml:

    <resources>
        <resource>
            <key>fileMenuCaption</key>
            <value>File</value>
        </resource>
        <resource>
            <key>editButtonCaption</key>
            <value>Edit</value>
        </resource>
    </resources>

Resource files are named according to the two-character language code for the language the resource file is for: "en" for English, "fr" for French, etc. For a user who wants to see English, resources.en.xml is used. Only languages that have resource files are available to users. Search the Internet for "ISO 639-1" to find a list of language codes.

To create resources in a different language, copy the contents of resources.en.xml in the Resources folder to another file with the appropriate name, such as resources.fr.xml for French. For each key-value pair in the file, replace the value with the equivalent in the desired language. For example, here's what part of resources.fr.xml would look like:

    <resources>
        <resource>
            <key>fileMenuCaption</key>
            <value>Fichier</value>
        </resource>
        <resource>
            <key>editButtonCaption</key>
            <value>Modifier</value>
        </resource>
    </resources>

Project resource files are intended to supplement and override the values in the application resource files. One purpose is to provide translations for the table and field captions and data group and role names. By default, the captions and names entered into Studio are displayed to the user as is in the report writer. However, if you want a multi-lingual application, you probably also want the captions and names displayed in the user's language. To do that, create a resources file with the desired language code in the Project_Data folder. For example, if you wanted to create German translations for the field captions, create a resources.de.xml file in the Project_Data folder, and enter something like the following:

	<resources>
		<resource>
			<key>Category</key>
			<value>Kategorie</value>
		</resource>
		<resource>
			<key>Category ID</key>
			<value>Kategorie-ID</value>
		</resource>
		<resource>
			<key>Category Name</key>
			<value>Kategorie Name</value>
		</resource>
	</resources>

Another purpose of project resource files is to the override the values in the application resource files. For example, if you'd rather display "Data group" as "Module," you could edit these entries in resources.en.xml in the Resources folder:

    <resource>
        <key>dataGroupCaption</key>
        <value>Data Group</value>
    </resource>
    <resource>
        <key>datagroupsInRoleCaption</key>
        <value>Data Groups in role</value>
    </resource>
    <resource>
        <key>dataGroupsCaption</key>
        <value>Data Groups</value>
    </resource>

However, the next time a new version of Horizon Reports is released, resources.en.xml is overwritten with a new copy and your custom changes are lost. Instead, create a project resources file with just the entries you want to override; for example:

    <resources>
        <resource>
            <key>dataGroupCaption</key>
            <value>Module</value>
        </resource>
        <resource>
            <key>datagroupsInRoleCaption</key>
            <value>Modules in role</value>
        </resource>
        <resource>
            <key>dataGroupsCaption</key>
            <value>Modules</value>
        </resource>
    </resources>

If you want to programmatically get a specific resource in the language for the current user, use code like the following:

```csharp
string resource = Application.Localizer.LanguageResources["keyValue"];
```

where "keyValue" is the resource key. To specify a different language, use something like:

```csharp
string key = "langCode" + Application.Localizer.LanguageSeparator +
    "keyValue";
string resource = Application.Localizer.LanguageResources[key];
```

where "langCode" is the language code, such as "de" for German.

Horizon Reports also supports locale-specific resource files such as resources.FR-fr.xml. If present, they take top priority over language resources.