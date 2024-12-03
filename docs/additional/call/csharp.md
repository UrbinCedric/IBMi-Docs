# Calling IBM i with C# #

For this example, I will be using Dotnet Core.


## ODBC
The **IBM i ODBC driver** must be installed on your system.
Follow the [windows](https://barrettotte.github.io/IBMi-Book/#/additional/call/windows) or [linux](https://barrettotte.github.io/IBMi-Book/#/additional/call/linux) setup to continue.

I wrote the linux installation steps with C#, if that means anything.


## ODBC NuGet
The package reference ```System.Data.Odbc``` needs to be added to the **.csproj** file.

With **Dotnet Core CLI** you can install with the command ```dotnet add package System.Data.Odbc```.

```xml
 
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="System.Data.Odbc" Version="4.7.0"/>
  </ItemGroup>
</Project>
```


## Example Program
```cs
// Program.cs

using System.Data.Odbc;

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Setup connection
            var conn = new OdbcConnection("Driver={IBM i Access ODBC Driver};" + String.Format(
            "System={0};Uid={1};Pwd={2}", "MY400", "USER", "MYPASSWORD"));

            // Create SQL statement
            var sqlCmd = ibmi.Db2Conn.CreateCommand();
            sqlCmd.CommandText = @"
                SELECT TABLE_SCHEMA, TABLE_NAME, TABLE_PARTITION, SOURCE_TYPE
                FROM QSYS2.SYSPARTITIONSTAT WHERE TABLE_SCHEMA = 'OTTEB1'
                ORDER BY TABLE_PARTITION";

            // Execute
            var dbReader = sqlCmd.ExecuteReader();

            // Print the results
            int colCount = dbReader.FieldCount;
            for(int i = 0; i < colCount; i++){
                String col = dbReader.GetName(i);
                Console.Write(col + ",");
            }
            Console.WriteLine();

            while(dbReader.Read()){
                for(int i = 0; i < colCount; i++){
                    object obj = dbReader.GetValue(i);
                    String col = (obj == null ? "NULL" : obj.ToString());
                    Console.Write(col + ",");
                }
                Console.WriteLine();
            }

            // Cleanup objects
            dbReader.Close();
            sqlCmd.Dispose();
            conn.Close();
        }
    }
}
```

<br>

## Result
Not as "pretty" as the other ones, forgive my laziness :/
```
TABLE_SCHEMA,TABLE_NAME,TABLE_PARTITION,SOURCE_TYPE,
OTTEB1,QDDSSRC,ALDSPF,DSPF,
OTTEB1,QCLLESRC,CLFIZZBUZZ,CLLE,
OTTEB1,QCLLESRC,ECHO,CLLE,
OTTEB1,QCLLESRC,FIRSTCL,CLLE,
OTTEB1,QCMDSRC,FIZZBUZZ,CMD,
OTTEB1,QRPGSRC,HELLO,RPG,
OTTEB1,QCLLESRC,HELLOCL,CLLE,
OTTEB1,QCLLESRC,JOBINFO,CLLE,
OTTEB1,QDDSSRC,TODOLIST,,
OTTEB1,TODOLIST,TODOLIST,,
OTTEB1,QDDSSRC,TODO00S,,
```
