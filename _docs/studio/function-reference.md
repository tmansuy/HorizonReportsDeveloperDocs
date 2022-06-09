---
layout: default
title: Expressions and Functions Reference
nav_order: 15
parent: Horizon Reports Studio
---

## Expressions
An expression is something that can be evaluated to a value. Expressions may consist of literal values (such as "Hello" or the number 10), fields from a database (such as Customers.Company), operators (discussed below), or functions (also discussed below). For example, Left(Customers.Company, 5) is an expression that uses the Left function to give the first five letters of the Company field in the Customers table.

### Literals
Horizon Reports supports the following literals in expressions:

* Char: a character in single quotes, such as 'a.'

* String: surround string literals with double quotes. You can use "escape" characters for special values, such as "\n" for a new line.

* Boolean: "true" or "false", without quotes.

* Real: any number with a decimal point. Numbers are assumed to be double; use ToDecimal(value) to convert to decimal.

* Integer: any number without a decimal point.

* Hex: an integer constant can be specified in hex notation, such as 0xFF12 instead of 65298.

* Null: use the keyword "null" (without quotes) for a null value.

* DateTime: surround a valid .NET DateTime pattern with "#" characters; for example, #03/02/2010#.

* TimeSpan: use a string in the format ##[d.]hh:mm[:ss[.ff]]#. For example, #03/02/2010# + ##1.23:45#.

### Operators
Horizon Reports supports the four basic arithmetic operators&mdash;addition (+), subtraction (-), multiplication (*), and division (/)&mdash;as well as the modulus (%) and power (^) operators. (In case you've forgotten, the modulus operator divides one numeric value by another and returns the remainder; 99 % 5 is 4). Here's an example:

    a*2 + b^2 - 99%5

If a is 5 and b is 3, the result is 15: 5*2 (10) + b^2 (9) - 99%5 (4).

The four comparison operators&mdash;equals (=), not equals (<>), less than (<), and greater than (>)&mdash;are supported as well.

Horizon Reports supports the And, Or, Xor, and Not operators for both logical and bitwise operations. If both operands are Booleans, the operation is logical. If both are integers, the operation is bitwise. Any other combination results in an error. Here's an example of a logical operation:

    a > 100 And Not b = 100

If a is 150 and b is 3, the result is true.

Here's a bitwise operation:

    (100 Or 2) And 1

The result is 0.

The left (<&lt;) and right (>&gt;) shift operators do a bitwise shift and are only valid on integers. For example:

    100 >> 2

gives 25.

The + operator also serves as the string concatenation operator. It is valid even if only one operand is a string; the non-string operand is automatically converted to a string. For example:

    "abc" + "def"
    "the number is: " + 100

The syntax for the indexing operator is memberName[indexExpression], where memberName is the name of a member of the class the function belongs to. Any expression can appear inside the brackets. Here's an example:

    MyArray[i + 1] + 100

The in operator returns true if a value is contained within a set of items. Its syntax is either:

    VALUE in (ITEM1, ITEM2, ... )

or

    VALUE in COLLECTION

where COLLECTION is an array or implements the .NET ICollection<T>, IDictionary<K,V>, IList, or IDictionary interfaces.

For example, if SomeDate is 03/15/2004, Month(SomeDate) in (1, 2, 3) returns true (the Month function returns the month number of the specified date).

## Functions
Functions are specified as the function name (note that function names are case-insensitive) followed by left and right parentheses. Parameters (values for the function to work on) may be specified inside the parentheses, and may be literal values, fields from a database, or another expression (such as Year(Now())).

There are many functions built into Horizon Reports. These functions are very similar to the equivalent functions in Microsoft Excel, in terms of the function names, the parameters they take, and the values they return. There are also functions that have the same names as those in earlier versions of Horizon Reports for backward compatibility. You can, of course, also create your own functions using a [functions plugin](vfps://Topic/_0SK0XEC3O).

Here is a list of the functions built into the report writer.

**Abs( NUMERIC_VALUE )**

Returns the absolute value of the specified numeric expression.

Abs(-6.5) returns 6.5.

**AddDays( DATE_VALUE, NUMERIC_VALUE )**

Adds the specified number of days to the specified date.

If Orders.OrderDate contains 01/01/2014, AddDays(Orders.OrderDate, 15) returns 01/15/2015.

**AllTrim( STRING )**
This function is the same as Trim and is provided for backward compatibility.

**AScan( ARRAY, VALUE )**
This function is the same as Match, although the order of the parameters is reversed, and is provided for backward compatibility.

**At( STRING_TO_FIND, STRING_TO_SEARCH_IN )**
Returns the position at which STRING_TO_FIND is found within STRING_TO_SEARCH_IN or -1 if it isn't found. The position is zero-based, so Find returns 0 if STRING_TO_FIND is found at the start of STRING_TO_SEARCH_IN. At is case-sensitive; use the Atc function for case-insensitive searches.

At("soft", "Microsoft") returns 5 and At("soft", "MicroSoft") returns -1 (because of the capital "S"). At("Micro", "Microsoft") returns 0 while At("mega", "Microsoft") returns -1.

**Atc( STRING_TO_FIND, STRING_TO_SEARCH_IN )**
A case-insensitive version of At.

Atc("soft", "Microsoft") and At("soft", "MicroSoft") both return 5.

**Cast( VALUE, TYPE )**
Converts an expression from one data type to another.

Cast(Customers.Type, int) returns 5 if Customers.Type contains the string "5."

**Ceiling( NUMERIC_VALUE )**
Returns the next highest integer that is greater than or equal to the specified value.

If SomeValue is 17.6, Ceiling(SomeValue) returns 18.

**Char( INTEGER_VALUE )**
Returns the character whose numeric ASCII code is the parameter. The parameter must be between 0 and 255.

Char(65) returns "A."

**Chr( INTEGER_VALUE )**
This function is the same as Char and is provided for backward compatibility.

**CMonth( DATE_VALUE )**
This function is the same as MonthName and is provided for backward compatibility.

**CToD( VALUE )**
This function is the same as DateValue and is provided for backward compatibility.

**Date( YEAR, MONTH, DAY)**
Converts the year, month, and day (which are specified as numeric values) into a date value.

Date(2004, 3, 30) returns 03/30/2004 as a date.

**Date()**
This function is the same as Now and is provided for backward compatibility.

**DateDiff( END_DATE, START_DATE )**
Returns the number of days between the specified dates.

If SomeDate1 is 03/30/2004 and SomeDate2 is 04/01/2004, DateDiff(SomeDate2, SomeDate1) gives 2.

**DateValue( VALUE )**
Converts the specified string into a datetime value. See the <a href="http://msdn.microsoft.com/en-us/library/system.datetime.parse.aspx#StringToParse" target="top">MSDN web site</a> for the type of strings that can be converted.

If SomeDate is "03/30/2004", DateValue(SomeDate) returns 03/30/2004 as a DateTime value.

**Day( DATE_VALUE )**
Returns the day part of the date parameter as a numeric value from 1 to 31.

If SomeDate is 03/30/2004, Day(SomeDate) returns 30.

**EDate( DATE_VALUE, NUMBER_OF_MONTHS )**
Returns a date the specified number of months from the date parameter. If NUMBER_OF_MONTHS is a positive value, a date after the specified date is returned; use a negative value to obtain a date before the specified date.

If SomeDate is 03/31/2004, EDate(SomeDate, -1) returns 02/29/2004 and EDate(SomeDate, 1) returns 04/30/2004.

**Empty( VALUE )**
Determines whether an expression evaluates to empty.

If SomeText is "hello" and SomeOtherText is "", Empty(SomeText) returns false and Empty(SomeOtherText) returns true.

**EndOfMonth( DATE_VALUE )**
Returns the last day of the month the specified date is in.

If SomeDate is 02/15/2009, EndOfMonth(SomeDate) returns 02/28/2009.

**Find( STRING_TO_FIND, STRING_TO_SEARCH_IN [, START_POSITION] )**
Returns the position at which STRING_TO_FIND is found within STRING_TO_SEARCH_IN or -1 if it isn't found. The position is zero-based, so Find returns 0 if STRING_TO_FIND is found at the start of STRING_TO_SEARCH_IN. The optional START_POSITION parameter specifies the starting position to search from. Find is case-sensitive; use the Search function for case-insensitive searches.

Find("soft", "Microsoft") returns 5 and Find("soft", "MicroSoft") returns -1 (because of the capital "S"). Find("Micro", "Microsoft") returns 0 while Find("mega", "Microsoft") returns -1.

**FirstOfMonth( DATE_VALUE )**
Return the first day of the month the specified date is in.

If SomeDate is 03/15/2009, FirstOfMonth(SomeDate) returns 03/01/2009.

**Floor( NUMERIC_VALUE )**
Returns the nearest integer that is less than or equal to the specified value.

If SomeValue is 17.6, Floor(SomeValue) returns 17.

**GetParameter( NAME, CAPTION, TYPE, DEFAULT )**
Prompts the user for a value of the specified data type. This is similar to the ask-at-runtime condition dialog except the value is used in the expression of a formula. If you call the function more than once with the same name, the user isn't prompted again; instead, the value they enter the first time is returned.

NAME is the name of the parameter and CAPTION is the caption displayed to the user. TYPE is the data type with quotes around it, such as "String" for a string, "DateTime" for a DateTime value, "Int32" for an integer, and "Decimal" for a numeric value. DEFAULT is the default value; use "" if there is no default.

GetParameter("FiscalYear", "Current fiscal year", "Int32", "") returns whatever value the user enters.

**GoMonth( DATE_VALUE, NUMBER_OF_MONTHS )**
This function is the same as EDate and is provided for backward compatibility.

**ICase( EXPRESSION1, TRUE_RESULT1, EXPRESSION2, TRUE_RESULT2, ..., FALSE_RESULT )**
If EXPRESSION1 is True, ICase returns TRUE_RESULT1. If not and EXPRESSION2 is True, ICase returns TRUE_RESULT2. Up to five expression/true result pairs are allowed. If none of the expressions is true, ICase returns FALSE_RESULT.

If SomeDate is 03/15/2004, ICase(Month(SomeDate) = 1, "January", Month(SomeDate) = 2, "February", , Month(SomeDate) = 3, "March", "Some Other Month")) returns "March."

**If( EXPRESSION, TRUE_RESULT, FALSE_RESULT )**
If EXPRESSION is True, If returns TRUE_RESULT. Otherwise, it returns FALSE_RESULT. If statements can be nested if necessary but ICase is more efficient and less to type.

If SomeDate is 03/15/2004, If(Month(SomeDate) = 1, "January", "Some Other Month")) returns "Some Other Month."

**IIf( EXPRESSION, TRUE_RESULT, FALSE_RESULT )**
This function is the same as If and is provided for backward compatibility.

**InList( VALUE, LISTVALUE1, LISTVALUE2, LISTVALUE3 ... )**
Determines if a set of values contains the specified value.

If MyField contains "C", InList(MyField, "A", "B", "C", "D", "E") returns true.

**Int( NUMERIC_VALUE )**
Returns the integer portion of a numeric value, rounding up or down as necessary.

If SomeValue is 17.6, Int(SomeValue) returns 18.

**Left( STRING, NUM_CHARS )**
Returns the specified number of characters from the parameter, beginning at the first character on the left.

Left("Microsoft Windows", 5) returns "Micro."

**Len( STRING )**
Returns the number of characters in the parameter.

Len("Microsoft Windows") returns 17.

**Lower( STRING )**
Converts a character string to lowercase.

Lower("Microsoft Windows") returns "microsoft windows."

**LTrim( STRING )**
Removes blanks from the beginning of the parameter.

LTrim("&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This is a test&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;") returns "This is a test&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"

**LTrim( STRING, CHAR1, CHAR2, CHAR3 ... )**
Removes all instances of the specified characters from the beginning of the parameter.

LTrim("&nbsp;00&nbsp;&nbsp;&nbsp;This is a test&nbsp;&nbsp;&nbsp;&nbsp;", '&nbsp;', '0') returns "This is a test&nbsp;&nbsp;&nbsp;&nbsp;"

**Match( VALUE, ARRAY )**
Returns the position a value is found at in an array, or -1 if the value isn't found. The value is zero-based, meaning the first element of the array is 0, the second is 1, and so forth.

If MyArray is an array of 3, 5, 2, 1, 4, Match(5, MyArray) returns 1.

**Max( VALUE1, VALUE2, VALUE3, ... )**
Returns the largest of a set of values.

Max(3, 4, 2, 5, -17) returns 5.

**Mid( STRING, START_POSITION [, NUM_CHARS] )**
A substring of the string value, starting from START_POSITION (the first character is position 0, the second position 1, and so on). NUM_CHARS is optional: if it isn't specified, all characters starting from START_POSITION to the end of the string are returned. If it is specified, NUM_CHARS starting from START_POSITION are returned.

Mid("Microsoft Windows", 5) returns "soft Windows."
Mid("Microsoft Windows", 5, 4) returns "soft."

**Min( VALUE1, VALUE2, VALUE3, ... )**
Returns the smallest of a set of values.

Min(3, 4, 2, 5, -17) returns -17.

**Month( DATE_VALUE )**
Returns the month part of the date parameter as a numeric value.

If SomeDate is 03/30/2004, Month(SomeDate) returns 3.

**MonthName( DATE_VALUE )**
Returns the month name of the date parameter.

If SomeDate is 03/30/2004, MonthName(SomeDate) returns "March."

**Now()**
Returns the current date and time as a DateTime value.

**PadL( STRING, LENGTH [, CHAR] )**
Returns a string, padded with spaces or characters on the left to a specified length.

If SomeValue is "Windows," PadL(SomeValue, 10) is "&nbsp;&nbsp;&nbsp;Windows" and PadL(SomeValue, 10, 'a') is "aaaWindows."

**PadR( STRING, LENGTH [, CHAR] )**
Returns a string, padded with spaces or characters on the right to a specified length.

If SomeValue is "Windows," PadR(SomeValue, 10) is "Windows&nbsp;&nbsp;&nbsp;" and PadR(SomeValue, 10, 'a') is "Windowsaaa."

**Proper( STRING )**
Converts a character string to title case (the first letter of each word is capitalized).

Proper("microsoft windows") returns "Microsoft Windows."

**Replace( OLD_TEXT, START, NUM_CHARS_TO_REPLACE, REPLACEMENT )**
Returns a string created by replacing a specified number of characters in a string with another string. START specifies the position in OLD_TEXT where the replacement begins (remembering that the first character is 0, the second is 1, and so on), NUM_CHARS_TO_REPLACE specifies the number of characters to be replaced (if it's 0, the replacement string is inserted into OLD_TEXT), and REPLACEMENT specifies the replacement string (if it's the empty string, the number of characters specified by NUM_CHARS_TO_REPLACE are removed from OLD_TEXT).

If SomeValue is "The quick brown fox", Replace(SomeValue, 4, 5, "slow") returns "The slow brown fox."

**Replicate( STRING, NUMBER_OF_TIMES )**
This function is the same as Rept and is provided for backward compatibility.

**Rept( STRING, NUMBER_OF_TIMES )**
Repeats the specified string the specified number of times.

Rept("The", 5) returns "TheTheTheTheThe."

**Right( STRING, NUM_CHARS )**
Returns the specified number of rightmost characters from a character string.

Right("Microsoft Windows", 5) returns "ndows."

**Round( NUMERIC_VALUE, NUMBER_OF_DIGITS )**
Returns a numeric value rounded to a specified number of decimal places.

If SomeValue contains 17.567, Round(SomeValue, 2) returns 17.57.

**Search( STRING_TO_FIND, STRING_TO_SEARCH_IN [, START_POSITION] )**
Returns the position at which STRING_TO_FIND is found within STRING_TO_SEARCH_IN or -1 if it isn't found. The position is zero-based, so Search returns 0 if STRING_TO_FIND is found at the start of STRING_TO_SEARCH_IN. The optional START_POSITION parameter specifies the starting position to search from. Search is case-insensitive; use the Find function for case-sensitive searches.

Search("soft", "Microsoft") and Search("soft", "MicroSoft") both return 5 (the second example has a capital "S" but Search is case-insensitive). Search("Micro", "Microsoft") returns 0 while Search("mega", "Microsoft") returns -1.

**Str( VALUE )**
Converts the parameter into the equivalent string. This is the equivalent of cast(VALUE, String).

If SomeValue is 20, Str(SomeValue) returns "20."

**StrTran( TEXT, FIND_VALUE, [, REPLACE_VALUE [, START_OCCURRENCE , NUM_OF_OCCURRENCES , FLAGS ]] )**
Returns a string created by replacing one string within a string with another string. FIND_VALUE specifies the text to find within TEXT. REPLACE_VALUE is the string to replace FIND_VALUE with; if isn't specified, FIND_VALUE is removed from TEXT. The START_OCCURRENCE and NUM_OF_OCCURRENCES parameters are ignored as they're for backward compatibility only. Specify a non-zero value for FLAGS to perform a case-insensitive search.

If SomeValue is "The quick brown fox", StrTran(SomeValue, "quick", "slow") returns "The slow brown fox."
If SomeValue is "The quick brown fox", StrTran(SomeValue, "QUICK", "slow", -1, -1, 1) returns "The slow brown fox."

**Stuff( OLD_TEXT, START, NUM_CHARS_TO_REPLACE, REPLACEMENT )**
This function is the same as Replace and is provided for backward compatibility.

**Substitute( TEXT, FIND_VALUE, REPLACE_VALUE )**
Searches the first parameter for occurrences of the second and replaces each occurrence with the third. Specify an empty string to remove FIND_VALUE from TEXT.

Substitute("Microsoft Windows", "Micro", "Mega") returns "Megasoft Windows."

**Substr( STRING, START_POSITION [, NUM_CHARS] )**
This function is the same as Mid and is provided for backward compatibility.

**Text( VALUE [, FORMAT] )**
Converts the parameter into the equivalent string. This is the equivalent of cast(VALUE, String). If the optional FORMAT parameter is specified, it indicates how to do the conversion; see the <a href="http://msdn.microsoft.com/en-us/library/system.string.format.aspx" target="top">MSDN web site</a> for the type of formats that can be specified.

If SomeValue is 20, Text(SomeValue) returns "20" and Text(SomeValue, "There are {0} items") returns "There are 20 items."

**ToDecimal( VALUE )**
Converts a double value to a decimal value. This is usually needed in an expression when multiplying a literal value like 0.05 by a decimal value.

Quantity * UnitPrice * ToDecimal(0.05) returns 5% of the product of Quantity and UnitPrice.

**ToDouble( VALUE )**
Converts a decimal value to a double value. This is usually needed in an expression when multiplying a field containing double values by a decimal value.

ToDouble(Quantity * UnitPrice) * 0.05 returns 5% of the product of Quantity and UnitPrice.

**Trim( STRING )**
Removes all blanks from both the beginning and the end of the parameter.

Trim("&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This is a test&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;") returns "This is a test"

**Upper( STRING )**
Converts a character string to uppercase.

Upper("Microsoft Windows") returns "MICROSOFT WINDOWS"

**Val( STRING )**
This function is the same as Value and is provided for backward compatibility.

**Value( STRING )**
Converts a string value to a numeric value.

If SomeString is "10", Value(SomeString) returns 10

**Year( DATE_VALUE )**
Returns the year part of the date parameter as a numeric value.

If SomeDate is 03/30/2004, Year(SomeDate) returns 2004
