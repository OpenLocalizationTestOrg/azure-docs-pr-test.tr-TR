---
title: "C# uygulamasından PostgreSQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, PostgreSQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz bir C# (.NET) kod örneği sağlanmıştır."
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
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="1fe63-103">PostgreSQL için Azure Veritabanı: Bağlanmak ve veri sorgulamak için .NET'i (C#) kullanma</span><span class="sxs-lookup"><span data-stu-id="1fe63-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="1fe63-104">Bu hızlı başlangıçta, C# uygulaması kullanılarak PostgreSQL için Azure Veritabanı'na nasıl bağlanılacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1fe63-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="1fe63-105">Ayrıca veritabanında veri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerini nasıl kullanacağınız da gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1fe63-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="1fe63-106">Bu makaledeki adımlarda, C# kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve PostgreSQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fe63-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1fe63-107">Prerequisites</span></span>
<span data-ttu-id="1fe63-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="1fe63-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1fe63-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="1fe63-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="1fe63-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="1fe63-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="1fe63-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1fe63-111">You also need to:</span></span>
- <span data-ttu-id="1fe63-112">[.Net Framework](https://www.microsoft.com/net/download)'ü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="1fe63-113">NET’i platformunuza (Windows, Ubuntu Linux veya macOS) özel olarak yüklemek için bağlantılı makaledeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="1fe63-114">Kod yazmak ve düzenlemek için [Visual Studio](https://www.visualstudio.com/downloads/) veya Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="1fe63-115">Aşağıda açıklanan şekilde [Npgsql](http://www.npgsql.org/doc/index.html) kitaplığını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="1fe63-116">Visual Studio çözümünüze Npgsql başvuruları yükleme</span><span class="sxs-lookup"><span data-stu-id="1fe63-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="1fe63-117">C# uygulamasından PostgreSQL'e bağlanmak için Npgsql adlı açık kaynak ADO.NET kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="1fe63-118">NuGet bu başvuruları kolayca indirmenize ve yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1fe63-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="1fe63-119">Yeni bir C# çözümü oluşturun veya var olan bir çözümü açın:</span><span class="sxs-lookup"><span data-stu-id="1fe63-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="1fe63-120">Visual Studio'da Dosya menüsü **Yeni** > **Proje**'ye tıklayarak çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1fe63-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="1fe63-121">Yeni Proje iletişim kutusunda **Şablonlar** > **Visual C#** öğesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="1fe63-122">**Konsol Uygulaması (.NET Core)** gibi uygun bir şablon seçin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="1fe63-123">Npgsql'i yüklemek için NuGet Paket Yöneticisi'ni kullanın:</span><span class="sxs-lookup"><span data-stu-id="1fe63-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="1fe63-124">**Araçlar** menüsü > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="1fe63-125">**Paket Yöneticisi Konsolu**'nda şu komutu yazın: `Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="1fe63-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="1fe63-126">install komutu Npgsql.dll'yi ve ilgili derlemeleri indirir ve bunları bağımlılık olarak çözüme ekler.</span><span class="sxs-lookup"><span data-stu-id="1fe63-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="1fe63-127">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="1fe63-127">Get connection information</span></span>
<span data-ttu-id="1fe63-128">PostgreSQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1fe63-129">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1fe63-130">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1fe63-131">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **mypgserver-20170401**) arayın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="1fe63-132">**mypgserver-20170401** sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="1fe63-133">Sunucunun **Genel Bakış** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="1fe63-134">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1fe63-135">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="1fe63-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="1fe63-136">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="1fe63-137">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="1fe63-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="1fe63-138">Bağlanıp **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini kullanarak verileri yüklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="1fe63-139">Kod, [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) yöntemiyle birlikte NpgsqlCommand sınıfını kullanarak PostgreSQL ile bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="1fe63-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="1fe63-140">Ardından kod [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) yöntemini kullanarak CommandText özelliğini ayarlar ve [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) yöntemini çağırarak veritabanı komutlarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="1fe63-141">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        // Obtain connection string information from the portal
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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="1fe63-142">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="1fe63-142">Read data</span></span>
<span data-ttu-id="1fe63-143">Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="1fe63-144">Kod, [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) yöntemiyle birlikte NpgsqlCommand sınıfını kullanarak PostgreSQL ile bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="1fe63-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="1fe63-145">Ardından kod [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) ve [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) yöntemini kullanarak veritabanı komutlarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="1fe63-146">Daha sonra kod [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) yöntemini kullanarak sonuçlardaki kayıtlara gider.</span><span class="sxs-lookup"><span data-stu-id="1fe63-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="1fe63-147">Ardından kod [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) ve [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) yöntemini kullanarak kayıttaki değerleri ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="1fe63-148">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        // Obtain connection string information from the portal
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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="1fe63-149">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1fe63-149">Update data</span></span>
<span data-ttu-id="1fe63-150">Bağlanmak ve **UPDATE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="1fe63-151">Kod, [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) yöntemiyle birlikte NpgsqlCommand sınıfını kullanarak PostgreSQL ile bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="1fe63-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="1fe63-152">Ardından kod [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) yöntemini kullanarak CommandText özelliğini ayarlar ve [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) yöntemini çağırarak veritabanı komutlarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="1fe63-153">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        // Obtain connection string information from the portal
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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="1fe63-154">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="1fe63-154">Delete data</span></span>
<span data-ttu-id="1fe63-155">Bağlanmak ve **DELETE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1fe63-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="1fe63-156">Kod, [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) yöntemiyle birlikte NpgsqlCommand sınıfını kullanarak PostgreSQL ile bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="1fe63-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="1fe63-157">Ardından kod [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) yöntemini kullanarak CommandText özelliğini ayarlar ve [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) yöntemini çağırarak veritabanı komutlarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1fe63-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="1fe63-158">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1fe63-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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
        // Obtain connection string information from the portal
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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="1fe63-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1fe63-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1fe63-160">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="1fe63-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
