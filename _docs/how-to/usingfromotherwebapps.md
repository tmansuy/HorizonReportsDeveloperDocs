---
layout: default
title: Using Horizon Reports from Web Applications
nav_order: 14
parent: How To
---

To display Horizon Reports from another web application, simply navigate the browser to the appropriate path. If you want to automatically log the user in, specify "username=*username*" and "password=*password*" in the URL, where *username* and *password* are the Horizon Reports user name and password, respectively.

If you're concerned about passing the user name and password in clear text, do one of the following.

### .NET environment

If you're accessing Horizon Reports from a .NET web application, call the static GenerateUserToken method of the static HorizonReports.Library.SecurityFunctions class, passing it the user name and password to log in as. This method returns a security token which is only good on the system it was generated on and only for 20 seconds. Then immediately navigate the browser to the appropriate path, specifying "token=*tokenstring*" in the URL, where *tokenstring* is the token returned from GenerateUserToken.

If the URL contains other sensitive information that you'd like to hide, you can also encrypt the entire query portion of it. To do that, call the EncryptQueryString method of the static HorizonReports.Library.SecurityFunctions class, passing it the entire query string to be encrypted. Then, navigate the browser to the appropriate path, specifying "enc=*encryptedvalue*" in the URL, where *encryptedvalue* is the encrypted string returned from EncryptQueryString.

### Other environment

If your development environment doesn't allow you to use the .NET API, you can make an HTTP GET request to https: //*site*/api/usertoken, where *site* is the URL for Horizon Reports. This route expects the request to contain an HTTP basic authentication header and uses those credentials to generate the returned token.

## Running a report
To automatically run a report, specify "ReportToRun=*reportID*" in the URL, where *reportID* is the ID of the report. You can get the ID by looking in the SFX file for the ID element or by using the ID property of the report object; it's a GUID that'll look something like "e7d51c47-2df0-4a44-b177-642023145557." Here's an example (note that most of token was omitted for brevity):

    https://www.MyReports.com?token=q4cXeJ%2BITa0n
      &ReportToRun=e7d51c47-2df0-4a44-b177-642023145557

To run a report and display only the preview window, not the rest of the report writer UI, use "ReportPreviewDirect/report" in the URL. Here's an example (note that most of token was omitted for brevity):

    https://www.MyReports.com/ReportPreviewDirect/report?token=q4cXeJ%2BITa0n
      &ReportToRun=e7d51c47-2df0-4a44-b177-642023145557

If you need to pass a value for an ask-at-runtime filter condition, you can add it to the URL as well. The syntax for this is:

    filterID=values

where *filterID* is the ID of the filter condition and *values* are the values for the condition. You can get the filter ID by looking in the SFX file for the filter condition with the fieldname element set to the desired field and then get the value of the ID element. For example, here's part of an SFX file:

    <filters>
      <filter>
        <id>56651a75-9202-41e6-bd4d-0302cb3ad6ec</id>
        <field>5aaaf3d2-7f08-43e4-96ce-cedd52a8ce98</field>
        <fieldname>Orders.OrderDate</fieldname>

In this case, the filter condition is on the Orders.OrderDate field, so if that's the correct condition, use 56651a75-9202-41e6-bd4d-0302cb3ad6ec (the value of the ID element) as the filter ID.

If you need to specify more than one value, such as for an Is Between or Is One Of condition, separate the values with commas.

For example, to set the value for a condition to the value "Reports":

    https://www.MyReports.com?username=admin&password=admin
      &reporttorun=146608a9-7af8-4810-b8be-88848ac795ae
      &8df41129-86be-4800-9a47-08495d6ec9e8=Reports

Here's an example with more than one value:

    https://www.MyReports.com?username=admin&password=admin
      &reporttorun=146608a9-7af8-4810-b8be-88848ac795ae
      &8df41129-86be-4800-9a47-08495d6ec9e8=Reports,Microsoft

For date values, use YYYY-MM-DD HH:MM:SS. For example:

    https://www.MyReports.com?username=admin&password=admin
    &reporttorun=146608a9-7af8-4810-b8be-88848ac795ae
      &8df41129-86be-4800-9a47-08495d6ec9e8=2014-1-1 00:00:00,2014-12-31 23:59:59
	  
## Exporting a report

To export a report to file without displaying any UI dialog, use "ReportPreviewDirect/export" in the URL. The same options for specifying credentials and filter options when running a report directly are also used when exporting. By default, a *pdf* file will be generated, but you can specify the *filetype* parameter if a different output type is required.

For example, to generate a csv file:

    https://www.MyReports.com/ReportPreviewDirect/export?username=admin&password=admin
      &reporttorun=146608a9-7af8-4810-b8be-88848ac795ae
      &filetype=csv

The available file types are:

* csv
* html
* bmp
* gif
* jpg
* png
* tiff
* mht
* pdf
* rtf
* text
* xlsx
* xlsxfullformat

## Displaying Horizon Reports in an IFrame
If you use the report writer inside an IFrame, you can subscribe to a new "bootstrapperDone" event with addEventListener. This event fires when the page has finished loading, and can be used to execute actions in the parent appication. Here's an example that puts the report writer UI into an IFrame and hides it until it's finished loading:

    <iframe id="reportAppFrame" src="https://myurl.com/reporting" style="visibility: hidden;"></iframe>

    window.addEventListener('bootstrapperDone', handler);

    function handler (e) {
    	$("#reportAppFrame").show();
    }
