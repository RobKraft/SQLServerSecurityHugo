+++
author = "Rob Kraft"
title = "All about CLR Apps"
date = "2022-03-28"
weight = 1
#description = "How to create and add a .Net CLR app."
tags = [
    "Security Reasons",
    "Security Roles",
    "2022.03"
]
+++

You have the ability to write applications in a .Net language such as C# and then call those applications from with SQL Server.  This ability can be very useful for some purposes, but it comes with three risks.
---[more](/blog/clrapps/)--- <!--more-->

If an exception occurs in the application that is not handled, it can cause your SQL Server instance to crash.  The code running the application from the DLL is loaded into the SQL Server memory space and essentially becomes part of the SQL Server program, opening the door to this risk.

The second risk comes from the possibility that hackers replace the DLL you created with one of their own.  Such an attack would be very sophisticated and would require targeting your SQL Server specifically, but it is a possibility.

The third risk comes from the enabling of "clr" applications within SQL Server that potentially allows hackers to add their own "clr enabled" applications to SQL Server.  

How does all of this work?  If you would like to try this yourself, follow these steps.

1. Create a .Net program

Using the latest version of Visual Studio, create a new project using the built-in "SQL Server" or "SQL Server Database Project" template.  The example below was named "clrEnabledTests" when created.  

Add a "New Item" to the project, and from the SQL Server group choose "SQL CLR C# Stored Procedure":
![demo](/images/blog/SQLServerCLREnabled.png)

Replace the default code in SqlStoredProcedure1.cs with this code:
```
using System.Data;
using System.Data.SqlTypes;
using System.Net;
using System.IO;
using Microsoft.SqlServer.Server;
using System.Text;

public partial class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void spSQLServerVersions()
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://sqlserverinspector.com/api/currentsqlserverversions/");
        request.Method = "GET";
        request.ContentLength = 0;
        request.Credentials = CredentialCache.DefaultCredentials;
        request.ContentType = "application/json";
        request.Accept = "application/json";

        string strContent = "";
        //strContent += "1. App Ran" + Environment.NewLine;
        using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
        {
            //strContent += "2. Got response" + Environment.NewLine;
            using (Stream receiveStream = response.GetResponseStream())
            {
                //strContent += "3. Read stream" + Environment.NewLine;
                using (StreamReader readStream = new StreamReader(receiveStream, Encoding.UTF8))
                {
                    //strContent += "4. read stream 2" + Environment.NewLine;
                    strContent += readStream.ReadToEnd();
                }
            }
        }
        //Main Logic Begins here    
        SqlPipe pipe = SqlContext.Pipe;
        SqlMetaData[] cols = new SqlMetaData[1];
        cols[0] = new SqlMetaData("FullJson", SqlDbType.VarChar, 8000);

        SqlDataRecord record = new SqlDataRecord(cols);
        record.SetSqlString(0, new SqlString(strContent));
        pipe.Send(record);
    }
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void spJustReturnAString()
    {
       
        string strContent = "Hello World";
 
        //Main Logic Begins here    
        SqlPipe pipe = SqlContext.Pipe;
        SqlMetaData[] cols = new SqlMetaData[1];
        cols[0] = new SqlMetaData("FullJson", SqlDbType.VarChar, 8000);

        SqlDataRecord record = new SqlDataRecord(cols);
        record.SetSqlString(0, new SqlString(strContent));
        pipe.Send(record);
    }
}
```
Notes about the code above:

* The code will ccall a REST API on the Internet to return JSON with the current version of each version of SQL Server.
* The code has some lines commented out, but can be uncommented if useful for debugging.
* The code creates a DataRecord with a single column named "FullJson" and uses the SqlPipe to send the response back to SQL Server.
* There are two functions in the above code, spSQLServerVersions and spJustReturnAString.  They are independent of each other and will be explained below.
* This code did not use HttpClient because I wanted to stick with using DLLs that were already loaded into memory by SQL Server.

Now we can open SQL Server Management Studio (SSMS) for the remaining steps.

The DLL (aka Assembly) we created was NOT created with a certificate or an asymmetric key.  This means that someone else could create a different DLL with the same name and SQL Server could load it instead.  That is considered a security risk.  

First of all, try running this command in SSMS after specifying the correct path to your DLL:

```
create ASSEMBLY SqlServerVersionsService     
        FROM 'C:\{%your path here%}\clrEnabledTests.dll'     
        WITH PERMISSION_SET = UNSAFE ; 
```
You may get this error:
```
Msg 10327, Level 14, State 1, Line 1
CREATE ASSEMBLY for assembly 'clrTest' failed because assembly 'clrTest' is not trusted. The assembly is trusted when either of the following is true: the assembly is signed with a certificate or an asymmetric key that has a corresponding login with UNSAFE ASSEMBLY permission, or the assembly is trusted using sp_add_trusted_assembly.
```
So, we could try replacing "UNSAFE" with "SAFE in the command:
```
create ASSEMBLY SqlServerVersionsService     
        FROM 'C:\{%your path here%}\clrEnabledTests.dll'     
        WITH PERMISSION_SET = SAFE ; 
```
And hopefully get this error:
```
Msg 10343, Level 14, State 1, Line 3
CREATE or ALTER ASSEMBLY for assembly 'clrEnabledTests' with the SAFE or EXTERNAL_ACCESS option failed because the 'clr strict security' option of sp_configure is set to 1. Microsoft recommends that you sign the assembly with a certificate or asymmetric key that has a corresponding login with UNSAFE ASSEMBLY permission. Alternatively, you can trust the assembly using sp_add_trusted_assembly.
```
This tutorial is intentionally walking through error conditions to help explain the risks and the SQL Configuration settings we may need to modify.

First of all, if you want to use common language runtime (CLR) assemblies (aka DLLs) in SQL Server, you need to enable that feature.  To enable CLR assemblies, run this command:
```
sp_configure 'clr enabled', 1;      
GO       
RECONFIGURE;       
GO  
```
"CLR Enabled" must be turned on in order to execute the code in the CLR Assemblies we load into SQL Server.

To load our assembly, the assembly must be cryptographically protected, or we must tell SQL Server that the database we are loading the assembly into can be trusted.  Trusting the database is riskier than cryptographically protecting the DLL because it allows any DLL added as an assembly to the database to be trusted.  But, it is the easier approach, so let's do it with this command:
```
ALTER DATABASE [%yourdatabasename%] SET TRUSTWORTHY ON; 
```

Now we can try adding our assembly again:
```
create ASSEMBLY SqlServerVersionsService     
        FROM 'C:\Users\robkr\Source\Repos\Database1\bin\Debug\clrEnabledTests.dll'     
        WITH PERMISSION_SET = UNSAFE ; 
```

CLR Assemblies can be marked [SAFE, EXTERNAL_ACCESS, or UNSAFE](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-assembly-transact-sql).  If marked SAFE, SQL Server will block the assembly from making calls to other services on the computer, network, or Internet.  Our is marked UNSAFE, so SQL Server will allow the DLL to do whatever it wants.

Now we need to create a stored procedure linked to that DLL
```
CREATE PROCEDURE dbo.spGetSQLVersions     
AS EXTERNAL NAME SqlServerVersionsService.StoredProcedures.spSQLServerVersions;
```
Now we are ready to execute it.
```
execute spGetSQLVersions
```
The results probably look like this:
![demo](/images/blog/SQLServerCLRQueryResults.png)
Not very pretty, but we can make it look better.  Lets use some of the JSON features built into SQL Server to format that JSON response:
```
declare @tempJson table (jsonData varchar(max));
insert @tempJson
execute spGetSQLVersions
DECLARE @json VARCHAR(MAX);
select @json= jsonData from @tempJson
select * from OPENJSON(@json)
  WITH (
    commonName VARCHAR(50) 'strict $.commonName',
    numericName VARCHAR(50) '$.numericName',
    rtm VARCHAR(50) '$.rtm',
    currentName VARCHAR(50) '$.currentName',
    currentv VARCHAR(50) '$.current'
  );
```
That looks much nicer:
![demo](/images/blog/SQLServerCLRQueryResults2.png "10x")

This program is calling a public API to bring back the current CU/Version of each version of SQL Server as JSON, and the query above is formatting the JSON result like a table.

Can we mark our Assembly as SAFE? Let's try it.  To do so, we need to drop our stored procedure and then drop our assembly, then re-add them.  But this time we will flag the Assembly as SAFE when we add it:
```
DROP PROCEDURE spGetSQLVersions
DROP ASSEMBLY SqlServerVersionsService
go
CREATE ASSEMBLY SqlServerVersionsService     
        FROM 'C:\Users\robkr\Source\Repos\Database1\bin\Debug\clrEnabledTests.dll'     
        WITH PERMISSION_SET = SAFE ; 
go
CREATE PROCEDURE dbo.spGetSQLVersions     
AS EXTERNAL NAME SqlServerVersionsService.StoredProcedures.spSQLServerVersions;
go
CREATE PROCEDURE dbo.spJustReturnAString     
AS EXTERNAL NAME SqlServerVersionsService.StoredProcedures.spJustReturnAString;
```
Then run our stored proc again:
```
EXECUTE spGetSQLVersions
```
Now you should get an error that looks like this:
```
Msg 6522, Level 16, State 1, Procedure spGetSQLVersions, Line 0 [Batch Start Line 46]
A .NET Framework error occurred during execution of user-defined routine or aggregate "spGetSQLVersions": 
System.Security.SecurityException: Request for the permission of type 'System.Net.WebPermission, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' failed.
System.Security.SecurityException: 
   at System.Security.CodeAccessSecurityEngine.Check(Object demand, StackCrawlMark& stackMark, Boolean isPermSet)
   at System.Security.CodeAccessPermission.Demand()
   at System.Net.HttpWebRequest.CheckConnectPermission(Uri uri, Boolean needExecutionContext)
   at System.Net.HttpWebRequest..ctor(Uri uri, ServicePoint servicePoint)
   at System.Net.HttpRequestCreator.Create(Uri Uri)
   at System.Net.WebRequest.Create(Uri requestUri, Boolean useUriBase)
   at StoredProcedures.spSQLServerVersions()
```
This happened because we told SQL Server that our Assembly was SAFE, which means that it is not going to try to call another service, but then when we ran our app it attempted to make a call to an endpoint on the Internet.

You may have noticed that we created a second stored procedure named spJustReturnAString from the same Assembly.  Let's try running it:

```
EXECUTE spJustReturnAString
```
That should have returned a "Hello World" message.  That stored procedure from the same assembly worked because it truly is SAFE.  And by SAFE, we mean that it did NOT attempt to make a call to another service, so SQL Server let it run.

In SQL Server 2017, Microsoft added another setting called "CLR STRICT SECURITY".  This is turned on by default and when turned on it treats all Assemblies as UNSAFE, even if they are marked SAFE.  This means the assembly needs a certificate or an asymmetric key to be added and called by the database, even if it doesn't make calls to external services.  **Unless the database is marked Trustworthy**

All the options get confusing:

* If CLR STRICT SECURITY is off, then you won't be able to add an Assembly MARKED UNSAFE in a database unless the database is marked Trustworthy, or the DLL has a certificate or an asymmetric key.
* If CLR STRICT SECURITY is on, then you won't be able to add an Assembly MARKED UNSAFE, SAFE, or EXTERNAL_ACCESS in a database unless the database is marked Trustworthy, or the DLL has a certificate or an asymmetric key.

In other words:

* CLR ENABLED must be turned on to use CLR Assemblies.
* If the database is marked TRUSTWORTHY:
  * You can add any Assembly.
  * The CLR Strict Security setting and PERMISSION_SET (SAFE, UNSAFE, and EXTERNAL_ACCESS) are ignored.
* If the database is not marked TRUSTWORTHY:
  * If CLR STRICT SECURITY is on
    * Then your Assembly must have a certificate or an asymmetric key.
  * If CLR STRICT SECURITY is off
    * Then your Assembly must have a certificate or an asymmetric key only if you choose the UNSAFE PERMISSION_SET when adding the Assembly.

An assembly marked SAFE or EXTERNAL_ACCESS does not require a certificate or an asymmetric key, but since CLR STRICT Security treats them all as UNSAFE, they are all required to have a certificate or an asymmetric key.

* To see an example of signing your Assembly, check out [this article](https://www.sqlshack.com/impact-clr-strict-security-configuration-setting-sql-server-2017/).
* [Microsoft guidance on adding keys to an Assembly](https://docs.microsoft.com/en-us/archive/blogs/dataaccesstechnologies/deploying-sql-clr-assembly-using-asymmetric-key)
* [CLR STRICT SECURITY](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/clr-strict-security)
* [Another exampled Calling a REST API](https://www.c-sharpcorner.com/article/calling-rest-api-service-from-sql-server-using-c-sharp-sql-clr/0)
* [Another CLR example on MsSQLTips](https://www.mssqltips.com/sqlservertip/7189/sql-server-clr-scalar-functions-net/)
