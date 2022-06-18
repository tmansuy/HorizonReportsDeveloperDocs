---
layout: default
title: Relation Properties
nav_order: 8
parent: Data Dictionary
grand_parent: Horizon Reports Studio
---

When you select a relation in Studio, an editor displays the properties for that relation.

Although SQL doesn't have the concept of one-to-many or child-parent relations, Horizon Reports has an easier time resolving the relationships required in a query if you specify which table is on the "many" side and which is on the "one" side of a relationship (or which is the parent and which is the child).

The properties displayed are:

![](/assets/images/relationprops.png)

* *Many ("Child") table*: select which table is on the "many" side of the relationship from the drop-down list of tables. 

* *One ("Parent") table*: select which table is on the "one" side of the relationship from the drop-down list of tables. 


A join can be defined as a list of field pairs, or as a SQL expression (complex join).

* *Fields*: if defining this join as a list of field pairs, use the *Add field pair to join* button to add as many pairs as you need for the join. Then, choose the fields from the Child and Parent tables for that pair. 

* *Complex join*: Enter the SQL expression for the relationship here. Field names should be fully aliased (that is, include the name of the table). If either the table or field name contains illegal SQL characters (such as spaces) or SQL keywords, place delimiters around the table or field name. Although it's not common, subqueries are supported in complex join expressions.

* *Join type*: select which type of join to use: inner, favor child, favor parent, or full. An inner join only selects those parent ("one") records with at least one matching child ("many") record. "Favor child" and "favor parent" create an outer join. The reason the terms "left outer" and "right outer" aren't used is because it depends on how the SQL statement is created: if the child table is listed first, "favor child" results in a left outer join. "Favor child" means you want child records regardless of whether a parent record exists or not, and "Favor parent" (more common) means you want parent records whether a child record exists or not. A full join gives records from both tables regardless of whether there are matching records in either table.

* *Join weight*: some applications, such as accounting systems, have large numbers of tables and complex relationships between them. As a result, there may be more than one "path" from one table to another, indirectly related, table. Consider the relationships shown below. There are two ways to get from Table A to Table D. However, if the preferred path is through Table B, you can tell the report writer that by setting the join weight for the relationship between Table C and Table D to a higher value (the lower the value, the more important the join).

    ![](/assets/images/relationtree.gif)

* *How to filter unfavored table*: in SQL, when you specify an outer join between tables, you're indicating that you want all records from the favored table whether there are matches in the unfavored table or not. If you add a filter condition on the unfavored table, SQL treats it like an inner join: now you only get records from the favored table that have matches in the unfavored table. Because that behavior is unexpected, the default is to move the filter condition to the JOIN clause so the unfavored table is filtered but unmatched records in the favored table are still included. However, there are times when the user doesn't want that behavior; they want unmatched records eliminated even though it's an outer join. So, you now have a choice about what to do with a filter conditions on the unfavored table:

    The choices for this setting are:

    * *Use default*: use the value of the [How to Filter Unfavored Tables by Default]({% link _docs/studio/configuration/configuration-settings.md %}) configuration setting. Having a global setting allows you to change the overall mechanism used for the project without having to set it for every relationship.

    * *Include in WHERE*: keep the filter condition in the WHERE clause for the SQL statement, so it acts like an inner join.

    * *Include in JOIN*: move the filter condition to the JOIN clause for the SQL statement, so it acts like an outer join.

    * *Use subquery*: this is for more complicated cases. In this case, a subquery is used for the entire join and filter conditions.

* *Version*: the relation's [version number]({% link _docs/studio/datadictionary/versioning.md %}). A blank value means the relation is not versioned: it appears in the report writer regardless of the version of the database. For a relation that isn't available in every version of the database, enter the version number followed by "+" to indicate the relation appears in that version and higher versions and should not be used in lower versions (that is, the relation was added in that version), "-" to indicate the relation appears in that version and lower versions and should not be used in higher versions (that is, the relation was removed in the next version), or no suffix to indicate the relation appears only in that version and should not be used in any other version. For example, "5.3+" indicates the relation is available starting in version 5.3 while "5.3-" indicates it was removed in version 5.4.

    Use a comma-delimited list of values if the relation was added in one version and later removed. For example, "5.3+,5.5-" means it was added in version 5.3 and removed in version 5.6.

    > @icon-info-circle Multiple relations between the same pair of tables are allowed if they have different version numbers.