
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="52719-101">C# programı örneği</span><span class="sxs-lookup"><span data-stu-id="52719-101">C# program example</span></span>

<span data-ttu-id="52719-102">Bu makalenin sonraki bölümlerinde Hello ADO.NET toosend Transact-SQL deyimleri toohello SQL veritabanı kullanan bir C# programı sunar.</span><span class="sxs-lookup"><span data-stu-id="52719-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="52719-103">Merhaba C# programı hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="52719-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="52719-104">[ADO.NET kullanarak tooour SQL veritabanına bağlanan](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="52719-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="52719-105">[Tablolar oluşturur](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="52719-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="52719-106">[T-SQL INSERT deyimleri vererek Hello tabloları verileri ile doldurur](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="52719-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="52719-107">[Bir birleştirme kullanımıyla veri güncelleştirmeleri](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="52719-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="52719-108">[Bir birleşim kullanarak verileri siler](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="52719-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="52719-109">[Bir birleştirme kullanımıyla veri satırları seçer](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="52719-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="52719-110">(Bu, herhangi bir geçici tablo tempdb üzerinden bırakır) hello bağlantıyı kapatır.</span><span class="sxs-lookup"><span data-stu-id="52719-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="52719-111">Merhaba C# programı içerir:</span><span class="sxs-lookup"><span data-stu-id="52719-111">hello C# program contains:</span></span>

- <span data-ttu-id="52719-112">C# kod tooconnect toohello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="52719-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="52719-113">Merhaba T-SQL kaynak kodunu döndüren yöntemler.</span><span class="sxs-lookup"><span data-stu-id="52719-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="52719-114">Merhaba T-SQL toohello veritabanı gönderme iki yöntem.</span><span class="sxs-lookup"><span data-stu-id="52719-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="52719-115">toocompile ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="52719-115">toocompile and run</span></span>

<span data-ttu-id="52719-116">Bu C# programı mantıksal bir .cs dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="52719-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="52719-117">Ancak burada hello program birkaç kod bloklarda fiziksel olarak ayrılır, toomake anlamak ve her daha kolay toosee engeller.</span><span class="sxs-lookup"><span data-stu-id="52719-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="52719-118">toocompile ve bu programı çalıştır, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="52719-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="52719-119">Visual Studio'da bir C# projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="52719-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="52719-120">Merhaba proje türü olmalıdır bir *konsol* uygulama gibi bir hiyerarşi aşağıdaki hello gelen: **şablonları** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="52719-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="52719-121">Merhaba dosyasındaki **Program.cs**, kod hello küçük starter satırları silme.</span><span class="sxs-lookup"><span data-stu-id="52719-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="52719-122">Program.cs içinde kopyalama ve yapıştırma her içinde blokları, aşağıdaki hello Burada sunulan aynı sıra hello.</span><span class="sxs-lookup"><span data-stu-id="52719-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="52719-123">Program.cs içinde düzenleme hello aşağıdaki değerleri hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="52719-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="52719-124">**cb. Veri kaynağı**</span><span class="sxs-lookup"><span data-stu-id="52719-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="52719-125">**CD. Kullanıcı Kimliği**</span><span class="sxs-lookup"><span data-stu-id="52719-125">**cd.UserID**</span></span>
   - <span data-ttu-id="52719-126">**cb. Parola**</span><span class="sxs-lookup"><span data-stu-id="52719-126">**cb.Password**</span></span>
   - <span data-ttu-id="52719-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="52719-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="52719-128">Bu hello derleme doğrulayın **System.Data.dll** başvuruluyor.</span><span class="sxs-lookup"><span data-stu-id="52719-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="52719-129">tooverify, hello genişletin **başvuruları** hello düğümünde **Çözüm Gezgini** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="52719-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="52719-130">Visual Studio'da toobuild hello programı tıklatın hello **yapı** menüsü.</span><span class="sxs-lookup"><span data-stu-id="52719-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="52719-131">Visual Studio'dan toorun hello programı tıklatın hello **Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="52719-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="52719-132">Merhaba rapor çıktısı cmd.exe penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="52719-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="52719-133">Merhaba T-SQL tooadd başında düzenleme hello seçeneğiniz  **#**  olarak geçici tablolarda oluşturur toohello tablo adları **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="52719-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="52719-134">Test veritabanı kullanılabilir olduğunda bu tanıtım amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="52719-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="52719-135">Merhaba bağlantı kapandığında geçici tabloları otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="52719-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="52719-136">Yabancı anahtarlar için tüm başvuruları geçici tablolar için zorunlu değildir.</span><span class="sxs-lookup"><span data-stu-id="52719-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="52719-137">C# blok 1: ADO.NET kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="52719-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="52719-138">Sonraki</span><span class="sxs-lookup"><span data-stu-id="52719-138">Next</span></span>](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="52719-139">C# blok 2: T-SQL toocreate tabloları</span><span class="sxs-lookup"><span data-stu-id="52719-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="52719-140">[Önceki](#cs_1_connect) &nbsp;  /  &nbsp; [sonraki](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="52719-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="52719-141">Varlık ilişki diyagramı (ERD)</span><span class="sxs-lookup"><span data-stu-id="52719-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="52719-142">Merhaba önceki CREATE TABLE deyimleri içeren hello **başvuruları** anahtar sözcüğü toocreate bir *yabancı anahtar* iki tablo arasındaki ilişki (FK).</span><span class="sxs-lookup"><span data-stu-id="52719-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="52719-143">Tempdb kullanıyorsanız, hello açıklama `--REFERENCES` başında tire çifti kullanarak anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="52719-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="52719-144">Sonraki hello iki tablo arasında hello ilişki görüntüler ERD'yi olduğu.</span><span class="sxs-lookup"><span data-stu-id="52719-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="52719-145">Merhaba hello #tabEmployee.DepartmentCode değerleri *alt* sütun değerlerdir sınırlı toohello hello #tabDepartment.Department mevcut *üst* sütun.</span><span class="sxs-lookup"><span data-stu-id="52719-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![ERD gösteren yabancı anahtar](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="52719-147">C# Blok 3: T-SQL tooinsert veri</span><span class="sxs-lookup"><span data-stu-id="52719-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="52719-148">[Önceki](#cs_2_createtables) &nbsp;  /  &nbsp; [sonraki](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="52719-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="52719-149">C# blok 4: T-SQL tooupdate katılma</span><span class="sxs-lookup"><span data-stu-id="52719-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="52719-150">[Önceki](#cs_3_insert) &nbsp;  /  &nbsp; [sonraki](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="52719-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="52719-151">C# blok 5: T-SQL toodelete katılma</span><span class="sxs-lookup"><span data-stu-id="52719-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="52719-152">[Önceki](#cs_4_updatejoin) &nbsp;  /  &nbsp; [sonraki](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="52719-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


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
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="52719-153">C# blok 6: T-SQL tooselect satırları</span><span class="sxs-lookup"><span data-stu-id="52719-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="52719-154">[Önceki](#cs_5_deletejoin) &nbsp;  /  &nbsp; [sonraki](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="52719-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="52719-155">C# blok 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="52719-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="52719-156">[Önceki](#cs_6_selectrows) &nbsp;  /  &nbsp; [sonraki](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="52719-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="52719-157">Bu yöntem tarafından hello yerleşik tasarlanmış toorun hello T-SQL SELECT deyimi olan **Build_6_Tsql_SelectEmployees** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="52719-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="52719-158">C# blok 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="52719-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="52719-159">[Önceki](#cs_6b_datareader) &nbsp;  /  &nbsp; [sonraki](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="52719-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="52719-160">Bu yöntem, hiçbir veri satırı dönmeden hello veri tabloların içeriğini değiştirme işlemleri için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="52719-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="52719-161">C# blok 8: Gerçek test çıktı toohello konsol</span><span class="sxs-lookup"><span data-stu-id="52719-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="52719-162">Önceki</span><span class="sxs-lookup"><span data-stu-id="52719-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="52719-163">Bu bölüm, gönderilen program toohello konsol hello hello çıkış yakalar.</span><span class="sxs-lookup"><span data-stu-id="52719-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="52719-164">Yalnızca hello GUID değerleri test çalışmaları arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="52719-164">Only hello guid values vary between test runs.</span></span>


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
