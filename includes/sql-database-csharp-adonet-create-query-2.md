
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>C# programı örneği

Bu makalenin sonraki bölümlerinde Hello ADO.NET toosend Transact-SQL deyimleri toohello SQL veritabanı kullanan bir C# programı sunar. Merhaba C# programı hello aşağıdaki eylemleri gerçekleştirir:

1. [ADO.NET kullanarak tooour SQL veritabanına bağlanan](#cs_1_connect).
2. [Tablolar oluşturur](#cs_2_createtables).
3. [T-SQL INSERT deyimleri vererek Hello tabloları verileri ile doldurur](#cs_3_insert).
4. [Bir birleştirme kullanımıyla veri güncelleştirmeleri](#cs_4_updatejoin).
5. [Bir birleşim kullanarak verileri siler](#cs_5_deletejoin).
6. [Bir birleştirme kullanımıyla veri satırları seçer](#cs_6_selectrows).
7. (Bu, herhangi bir geçici tablo tempdb üzerinden bırakır) hello bağlantıyı kapatır.

Merhaba C# programı içerir:

- C# kod tooconnect toohello veritabanı.
- Merhaba T-SQL kaynak kodunu döndüren yöntemler.
- Merhaba T-SQL toohello veritabanı gönderme iki yöntem.

#### <a name="toocompile-and-run"></a>toocompile ve çalıştırma

Bu C# programı mantıksal bir .cs dosyasıdır. Ancak burada hello program birkaç kod bloklarda fiziksel olarak ayrılır, toomake anlamak ve her daha kolay toosee engeller. toocompile ve bu programı çalıştır, aşağıdaki hello:

1. Visual Studio'da bir C# projesi oluşturun.
    - Merhaba proje türü olmalıdır bir *konsol* uygulama gibi bir hiyerarşi aşağıdaki hello gelen: **şablonları** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.
3. Merhaba dosyasındaki **Program.cs**, kod hello küçük starter satırları silme.
3. Program.cs içinde kopyalama ve yapıştırma her içinde blokları, aşağıdaki hello Burada sunulan aynı sıra hello.
4. Program.cs içinde düzenleme hello aşağıdaki değerleri hello **ana** yöntemi:

   - **cb. Veri kaynağı**
   - **CD. Kullanıcı Kimliği**
   - **cb. Parola**
   - **InitialCatalog**

5. Bu hello derleme doğrulayın **System.Data.dll** başvuruluyor. tooverify, hello genişletin **başvuruları** hello düğümünde **Çözüm Gezgini** bölmesi.
6. Visual Studio'da toobuild hello programı tıklatın hello **yapı** menüsü.
7. Visual Studio'dan toorun hello programı tıklatın hello **Başlat** düğmesi. Merhaba rapor çıktısı cmd.exe penceresinde görüntülenir.

> [!NOTE]
> Merhaba T-SQL tooadd başında düzenleme hello seçeneğiniz  **#**  olarak geçici tablolarda oluşturur toohello tablo adları **tempdb**. Test veritabanı kullanılabilir olduğunda bu tanıtım amacıyla yararlı olabilir. Merhaba bağlantı kapandığında geçici tabloları otomatik olarak silinir. Yabancı anahtarlar için tüm başvuruları geçici tablolar için zorunlu değildir.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>C# blok 1: ADO.NET kullanarak bağlanma

- [Sonraki](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>C# blok 2: T-SQL toocreate tabloları

- [Önceki](#cs_1_connect) &nbsp;  /  &nbsp; [sonraki](#cs_3_insert)

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a>Varlık ilişki diyagramı (ERD)

Merhaba önceki CREATE TABLE deyimleri içeren hello **başvuruları** anahtar sözcüğü toocreate bir *yabancı anahtar* iki tablo arasındaki ilişki (FK).  Tempdb kullanıyorsanız, hello açıklama `--REFERENCES` başında tire çifti kullanarak anahtar sözcüğü.

Sonraki hello iki tablo arasında hello ilişki görüntüler ERD'yi olduğu. Merhaba hello #tabEmployee.DepartmentCode değerleri *alt* sütun değerlerdir sınırlı toohello hello #tabDepartment.Department mevcut *üst* sütun.

![ERD gösteren yabancı anahtar](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>C# Blok 3: T-SQL tooinsert veri

- [Önceki](#cs_2_createtables) &nbsp;  /  &nbsp; [sonraki](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a>C# blok 4: T-SQL tooupdate katılma

- [Önceki](#cs_3_insert) &nbsp;  /  &nbsp; [sonraki](#cs_5_deletejoin)


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a>C# blok 5: T-SQL toodelete katılma

- [Önceki](#cs_4_updatejoin) &nbsp;  /  &nbsp; [sonraki](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>C# blok 6: T-SQL tooselect satırları

- [Önceki](#cs_5_deletejoin) &nbsp;  /  &nbsp; [sonraki](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a>C# blok 6b: ExecuteReader

- [Önceki](#cs_6_selectrows) &nbsp;  /  &nbsp; [sonraki](#cs_7_executenonquery)

Bu yöntem tarafından hello yerleşik tasarlanmış toorun hello T-SQL SELECT deyimi olan **Build_6_Tsql_SelectEmployees** yöntemi.


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a>C# blok 7: ExecuteNonQuery

- [Önceki](#cs_6b_datareader) &nbsp;  /  &nbsp; [sonraki](#cs_8_output)

Bu yöntem, hiçbir veri satırı dönmeden hello veri tabloların içeriğini değiştirme işlemleri için çağrılır.


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a>C# blok 8: Gerçek test çıktı toohello konsol

- [Önceki](#cs_7_executenonquery)

Bu bölüm, gönderilen program toohello konsol hello hello çıkış yakalar. Yalnızca hello GUID değerleri test çalışmaları arasında farklılık gösterir.


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
