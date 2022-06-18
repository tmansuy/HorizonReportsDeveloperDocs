---
layout: default
title: Customizing the Project
nav_order: 3
parent: Quick Start
---

The next step is customizing the reporting project created from your database. Which properties you customize depends on the type of data object:

* *Database*: if you don't want to use the same connection settings to connect to the database when running Horizon Reports as in Studio, change the properties for the database as necessary. See the [Database Properties]({% link _docs/studio/datadictionary/database-properties.md %}) topic for details.

* *Table*: the only property you need to fill in for a table is the caption, the descriptive heading the user sees rather than the real table name. There are other properties available as well, including Reportable, Data Group, and Roles. See the [Table Properties]({% link _docs/studio/datadictionary/table-properties.md %}) topic for a complete list.

* *Field*: at a minimum, fill in the Caption for each field. Other properties, such as Format, Reportable, Sortable, Filterable, and Expression, can be changed as necessary. See the [Field Properties]({% link _docs/studio/datadictionary/field-properties.md %}) topic for a complete list of the properties for a field.

* *Relation*: you need to define a relation for each pair of tables, specifying the tables, the fields to join them on (or the join expression if it's more complex than pairs of fields), and the join type. See the [Relation Properties]({% link _docs/studio/datadictionary/relation-properties.md %}) topic for more information.

You may also wish to define some calculated fields. A calculated field doesn't physically exist in the database, but is simply a formula that gives a value the user may want to query on. An example is the extended price of a sale item. This usually isn't stored because it's a derived value (price per item multiplied by the quantity sold), but the user may want it printed in a report or use it in a filter condition. So, you can define a calculated field in the appropriate table, specifying the caption, data type, and output expression (the formula) for the field. This field is then available for querying just like a real field&mdash;the user can include it in a report or filter on it&mdash;but internally, Horizon Reports uses the formula to derive the value.