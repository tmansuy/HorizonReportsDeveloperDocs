---
layout: default
title: Handling Optional Fields
nav_order: 9
parent: How To
---

Some applications allow users to create their own attributes for items. For example, the Sage 300 accounting system has an inventory control items table but doesn't have a field to store the color of an item. Fortunately, Sage 300 supports optional attribute fields, so the user can define Color as an optional field and enter a value for that field for each item.

Different systems implement optional attributes differently but typically there's a table containing metadata for the optional attributes (name, caption, data type, size, etc.) and a table containing the attribute values for each item. In the case of Sage 300, the table containing metadata is named CSOPTFH and it has OPTFIELD (name) and FDESC (caption) fields, and each entity table that supports optional fields, such as items, has a table containing the optional field values. In the case of the inventory items table, named ICITEM, the optional fields table is named ICITEMO and it has ITEMNO (item number), OPTFIELD (optional field name), TYPE (the data type of the value), and VALUE (a string value, hence the need for TYPE so the system knows how to convert the stored value into the correct data type).

To make it easier for the user to report on optional attributes, we recommend programmatically adding a field to the data dictionary for each attribute. The field should call a function from its Expression property that returns the value of the attribute for the current record.

Here's such a function that works with the Sage 300 ITEMNO optional fields table. It expects to be passed the item number to get the optional field for, the optional field name, and the data type code.

```csharp
/// <summary>
/// A cache of records from ICITEMO. Note that there is one dictionary
/// per data source.
/// </summary>
private static Dictionary<string, Dictionary<string, string>>
    _optionalFields =
    new Dictionary<string, Dictionary<string, string>>();

/// <summary>
/// A reference to the Stonefield Query application object.
/// </summary>
[Import]
public static IHorizonReportsAppService Application;

/// <summary>
/// GetOptionalField is called from the Expression of fields added to
/// the data dictionary in SampleApplicationPlugin.AfterLogin.
/// </summary>
/// <param name="itemNumber">
/// The item number of the current inventory item.
/// </param>
/// <param name="optionalField">
/// The name of the optional field to get the value for.
/// </param>
/// <param name="type">
/// The type of result to return.
/// </param>
/// <returns>
/// The optional field value if it's found or blank if not.
/// </returns>
public static object GetOptionalField(string itemNumber,
    string optionalField, int type)
{
    // Create a key by combining the item number and optional field
    // name.
    string key = itemNumber.PadLeft(20) + optionalField.PadLeft(20);

    // If we don't already have the lookup data for the current data
    /// source, retrieve it and add it to the cache. Note that we put
    /// the data into a dictionary for speed of looking up the key.
    IDataSource datasource =
        Application.ConnectionManager.DataSources.CurrentDatasource;
    Dictionary<string, string> data;
    if (!_optionalFields.ContainsKey(datasource.Name))
    {
        
        Application.Logger.Info("GetOptionalField function: getting lookup data");
        string select = "select ITEMNO, OPTFIELD, VALUE from ICITEMO";
        IDatabase database = Application.DataDictionary.Databases[0];
        IConnectionFactory factory = datasource[database];
        IConnection connection = factory.CreateConnection();
        DataTable dt = connection.ExecuteSQLStatement(select,
            new string[] { }, "", null);
        data = dt.AsEnumerable().ToDictionary(
            row => row["ITEMNO"].ToString().PadLeft(20) +
            row["OPTFIELD"].ToString().PadLeft(20),
            row => row["VALUE"].ToString());
        _optionalFields.Add(datasource.Name, data);
    }

    // Look for the specified values and get the found value. Convert
    // it to the appropriate data type.
    data = _optionalFields[datasource.Name];
    object result = "";
    if (data.ContainsKey(key))
    {
        switch (type)
        {
            case 1:
                result = data[key];
                break;
            case 3:
                result = DateTime.Parse(data[key]);
                break;
            case 6:
                result = Double.Parse(data[key]);
                break;
            case 8:
                result = Int32.Parse(data[key]);
                break;
            case 9:
                result = Boolean.Parse(data[key]);
                break;
            case 100:
                result = Decimal.Parse(data[key]);
                break;
            default:
                break;
        }
    }
    return result;
}
```

The following code, which is the [AfterSetup](vfps://Topic/_0W60XD3HQ) method of an [application plugin](vfps://Topic/_0SK0XF365), dynamically adds optional fields to the ICITEM table in the data dictionary:

```csharp
/// <summary>
/// Fired after the application object setup tasks are done. This
/// plugin programmatically adds fields to the ICITEM table in the
/// data dictionary at runtime to handle optional fields.
/// </summary>
/// <returns>
/// True if the application can start, false if not.
/// </returns>
public bool AfterSetup()
{
    Application.Logger.Info("My application plugin: adding optional fields " +
        "to ICITEM for all datasources");
    // The SQL statement to retrieve a list of the optional fields.
    string select = "select distinct CSOPTFH.OPTFIELD, " +
        "CPOPTFH.FDESC, ICITEMO.TYPE from ICITEMO " +
        "inner join CSOPTFH on CSOPTFH.OPTFIELD = ICITEMO.OPTFIELD";

    // Get a reference to the database and the ICITEM.ITEMNO field.
    IDatabase database = Application.DataDictionary.Databases[0];
    Field IDField = Application.DataDictionary.Fields["ICITEM.ITEMNO"];

    // Go through all the data sources.
    foreach (IDataSource datasource in
        Application.ConnectionManager.DataSources)
    {
        // Retrieve a list of the optional fields.
        IConnectionFactory factory = datasource[database];
        IConnection connection = factory.CreateConnection();
        DataTable optFields = connection.ExecuteSQLStatement(select,
            new string[] { }, "", null);

        // For each optional field, create a field object in the data
        // dictionary in the ICITEM table.
        // These fields call the GetOptionalField function.
        Application.Logger.DebugFormat("My application plugin: adding " +
            "optional fields for datasource = {0}", datasource.Name);
        foreach (DataRow row in optFields.Rows)
        {
            string description = row["FDESC"].ToString().Trim();
            string id = row["OPTFIELD"].ToString().Trim();
            int type = (int)row["TYPE"];
            logger.DebugFormat("Adding optional field: {0} ({1})",
                description, id);

            // Add the field to ICITEM if it isn't already there.
            string fieldName = "ICITEM.A" + id + datasource.Name;
            CalculatedField field =
                Application.DataDictionary.Fields[fieldName]
                as CalculatedField;
            if (field == null)
            {
                field = new CalculatedField(fieldName);
                Application.DataDictionary.Fields.Add(field);
                switch (type)
                {
                    case 1:
                        field.DataType = typeof(String);
                        break;
                    case 3:
                        field.DataType = typeof(DateTime);
                        break;
                    case 6:
                        field.DataType = typeof(Double);
                        field.Format = "{0:#,##0.00}";
                        break;
                    case 8:
                        field.DataType = typeof(Int32);
                        field.Format = "{0:#,##0}";
                        break;
                    case 9:
                        field.DataType = typeof(Boolean);
                        break;
                    case 100:
                        field.DataType = typeof(Decimal);
                        field.Format = "{0:c2}";
                        break;
                    default:
                        break;
                }
                field.ExpressionType = ExpressionTypes.Expression;
                field.Expression =
                    @"GetOptionalField(ICITEM.ITEMNO, """ +
                    id + @""", " + type.ToString() + ")";
                field.FieldList.Add(IDField);
            }
            field.Caption = description;
        }
    }
    Application.Logger.Info("My application plugin: finished adding optional fields");

    return true;
}
```
