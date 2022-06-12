---
layout: default
title: Functions
nav_order: 3
parent: Plugins
---

Functions can be used from any place in the report writer where an expression is used, such as:

* The Expression property of a calculated field or end-user formula.

* The Caption or Heading property of a field.

* The heading of a report.

There's no special requirements of function classes and methods other than that they be static.

If a function needs access to the Horizon Reports object model, such as because it needs to query the data source used for the application or needs to access the data dictionary, create a static property to contain a reference to the application object and use the [Import] attribute on it.

```csharp
using HorizonReports;

namespace MyFunctions
{
    public static class MyFunctions
    {
        /// <summary>
        /// A reference to the application object.
        /// </summary>
		[Import]
        public static IHorizonReportsAppService Application;

        /// <summary>
        /// This is some function.
        public static string HelloWorld()
        {
            return "Hello world";
        }
    }
}
```

Here's a sample functions class, taken from Samples\SamplePlugins\SampleFunctions\SampleFunctions.cs. A copy of the DLL created from this class is in the Samples\Sample Project\Functions folder because it provides functions used by a couple of fields in the sample project:

* GetTax is used in the Expression property of the [Order Details].tax calculated field to calculate the sales tax for an order item.

* GetCSZ is used in the Expression property of the Customers.csz calculated field to create a country-sensitive formatted address: for Germany, it's formatted as PostalCode City (such as "12209 Berlin") while for other countries it's City, PostalCode Region (such as Walla Walla, WA 99362).

```csharp
using System;

namespace SampleFunctions
{
    /// <summary>
    /// This class provides some functions used by the sample project.
    /// </summary>
    /// <remarks>
    /// It provides a simple example of how to write functions
    /// called from the Expression property of fields or other places
    /// such as field captions.
    /// </remarks>
    public static class SampleFunctions
    {
        /// <summary>
        /// Get the current tax rate.
        /// </summary>
        /// <returns>
        /// The current tax rate (hard-coded as 5%).
        /// </returns>
        public static decimal GetTaxRate()
        {
            return 0.05M;
        }

        /// <summary>
        /// Gets the tax on the specified amount.
        /// </summary>
        /// <param name="amount">
        /// The amount to calculate the tax for.
        /// </param>
        /// <returns>
        /// The tax (based on a hard-coded rate of 5%).
        /// </returns>
        public static decimal GetTax(decimal amount)
        {
            return GetTaxRate() * amount;
        }

        /// <summary>
        /// Combines the city, region, and postal code into a
        /// country-sensitive formatted address.
        /// </summary>
        /// <param name="city">
        /// The city.
        /// </param>
        /// <param name="region">
        /// The region (state, province, etc.)
        /// </param>
        /// <param name="postalCode">
        /// The postal or zip code.
        /// </param>
        /// <param name="country">
        /// The country.
        /// </param>
        /// <returns>
        /// The country-sensitive formatted address.
        /// </returns>
        /// <remarks>
        /// For Germany, the format is PostalCode City Region.
        /// For all other countries, it's City, Region
        /// PostalCode.
        /// </remarks>
        public static string GetCSZ(string city, string region,
            string postalCode, string country)
        {
            string useRegion = region == null ? "" : region;
            string result;
            if (country == "Germany")
            {
                result = postalCode + " " + city + " " + useRegion;
            }
            else
            {
                result = city + ", " + useRegion + " " + postalCode;
            }
            return result;
        }
    }
}

```

### Formatters
A special category of functions are called formatters. These functions are used to dynamically format a field's value in a report. For example, suppose you have a numeric field that contains the number of minutes a process takes but you want it displayed as HH:MM instead (for example, 65 should appear as 1:05). You can create a plugin function called, for example, GetHHMM, that returns the desired format. You would then specify that function in an expression in the Format property of the field as follows (the word "value" is a placeholder for the current value to format):

    {GetHHMM(value)}

The function must accept a single parameter of type object, do any necessary conversion, and return a string. It must also use the Formatter attribute with two or more parameters:

* The description to display to the user in the report writer

* The data type(s) of the field this formatter can be used with

That attribute is defined in the [HorizonReports.Api](https://www.nuget.org/packages/HorizonReports.Api/) so you'll need to add that package to the functions project.

Here's what the GetHHMM function that converts the number of minutes into HH:MM looks like:

```csharp
[Formatter("HH:MM", typeof(Int16))]
public static string GetHHMM(object minutes)
{
   TimeSpan span = TimeSpan.FromMinutes(Convert.ToInt32(minutes));
   return span.ToString(@"hh\:mm");
}
```

Any functions defined as formatters automatically appear in the Format drop-down list in the Field Properties dialog in the report writer so the user can choose them as well.
