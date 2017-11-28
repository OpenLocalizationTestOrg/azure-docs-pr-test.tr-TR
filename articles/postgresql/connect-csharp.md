---
title: "C# üzerinden PostgreSQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç PostgreSQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir C# (.NET) kod örneğini sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="d67b9-103">Azure veritabanı PostgreSQL için: kullanım .NET (C#) tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="d67b9-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="d67b9-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl bir C# uygulaması kullanarak PostgreSQL için.</span><span class="sxs-lookup"><span data-stu-id="d67b9-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="d67b9-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="d67b9-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d67b9-106">Merhaba bu makaledeki adımları kullanarak C# geliştirme ile tanıdık ve yeni tooworking Azure veritabanı PostgreSQL için sahip olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="d67b9-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d67b9-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d67b9-107">Prerequisites</span></span>
<span data-ttu-id="d67b9-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="d67b9-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d67b9-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="d67b9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="d67b9-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="d67b9-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="d67b9-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d67b9-111">You also need to:</span></span>
- <span data-ttu-id="d67b9-112">[.Net Framework](https://www.microsoft.com/net/download)'ü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="d67b9-113">(Windows, Ubuntu Linux veya macOS) platformunuz için özel olarak bağlı hello makale tooinstall .NET Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="d67b9-114">Yükleme [Visual Studio](https://www.visualstudio.com/downloads/) veya Visual Studio Code tootype ve düzenleme kod.</span><span class="sxs-lookup"><span data-stu-id="d67b9-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="d67b9-115">Aşağıda açıklanan şekilde [Npgsql](http://www.npgsql.org/doc/index.html) kitaplığını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="d67b9-116">Visual Studio çözümünüze Npgsql başvuruları yükleme</span><span class="sxs-lookup"><span data-stu-id="d67b9-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="d67b9-117">Merhaba C# uygulama tooPostgreSQL, gelen tooconnect Npgsql adlı hello açık kaynak ADO.NET kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d67b9-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="d67b9-118">NuGet indirin ve hello başvuruları kolayca yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d67b9-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="d67b9-119">Yeni bir C# çözümü oluşturun veya var olan bir çözümü açın:</span><span class="sxs-lookup"><span data-stu-id="d67b9-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="d67b9-120">Visual Studio'da Dosya menüsü **Yeni** > **Proje**'ye tıklayarak çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d67b9-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="d67b9-121">Hello yeni proje iletişim kutusu, genişletin **şablonları** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="d67b9-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="d67b9-122">**Konsol Uygulaması (.NET Core)** gibi uygun bir şablon seçin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="d67b9-123">Merhaba Nuget Paket Yöneticisi tooinstall Npgsql kullanın:</span><span class="sxs-lookup"><span data-stu-id="d67b9-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="d67b9-124">Merhaba tıklatın **Araçları** menü > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="d67b9-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="d67b9-125">Merhaba, **Paket Yöneticisi Konsolu**, türü`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="d67b9-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="d67b9-126">Merhaba komutu yüklemeleri hello Npgsql.dll ve ilgili derlemeleri yükleme ve bunları bağımlılık hello çözümü olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="d67b9-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d67b9-127">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d67b9-127">Get connection information</span></span>
<span data-ttu-id="d67b9-128">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="d67b9-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="d67b9-129">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="d67b9-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d67b9-130">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d67b9-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d67b9-131">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d67b9-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="d67b9-132">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d67b9-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="d67b9-133">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d67b9-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="d67b9-134">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="d67b9-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d67b9-135">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="d67b9-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="d67b9-136">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="d67b9-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d67b9-137">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="d67b9-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="d67b9-138">Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.</span><span class="sxs-lookup"><span data-stu-id="d67b9-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="d67b9-139">Hello kodu kullanan NpgsqlCommand sınıfı yöntemiyle [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish bağlantı tooPostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d67b9-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d67b9-140">Merhaba kod yöntemi kullanıyorsa [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello veritabanı komutları.</span><span class="sxs-lookup"><span data-stu-id="d67b9-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="d67b9-141">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="d67b9-142">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="d67b9-142">Read data</span></span>
<span data-ttu-id="d67b9-143">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d67b9-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d67b9-144">Hello kodu kullanan NpgsqlCommand sınıfı yöntemiyle [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish bağlantı tooPostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d67b9-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d67b9-145">Merhaba kod yöntemi kullanıyorsa [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) ve yöntemi [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello veritabanı komutları.</span><span class="sxs-lookup"><span data-stu-id="d67b9-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="d67b9-146">Kod kullanan'sonraki hello [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) hello sonuçlarında tooadvance toohello kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d67b9-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="d67b9-147">Merhaba kod kullanıyorsa [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) ve [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello hello kayıt değerleri.</span><span class="sxs-lookup"><span data-stu-id="d67b9-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="d67b9-148">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="d67b9-149">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d67b9-149">Update data</span></span>
<span data-ttu-id="d67b9-150">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d67b9-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d67b9-151">Hello kodu kullanan NpgsqlCommand sınıfı yöntemiyle [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish bağlantı tooPostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d67b9-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d67b9-152">Merhaba kod yöntemi kullanıyorsa [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello veritabanı komutları.</span><span class="sxs-lookup"><span data-stu-id="d67b9-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="d67b9-153">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="d67b9-154">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="d67b9-154">Delete data</span></span>
<span data-ttu-id="d67b9-155">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d67b9-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="d67b9-156">Hello kodu kullanan NpgsqlCommand sınıfı yöntemiyle [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish bağlantı tooPostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d67b9-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d67b9-157">Merhaba kod yöntemi kullanıyorsa [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello veritabanı komutları.</span><span class="sxs-lookup"><span data-stu-id="d67b9-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="d67b9-158">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d67b9-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("DELETE FROM inventory WHERE name = {0};",
                "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d67b9-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d67b9-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d67b9-160">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="d67b9-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
