---
title: "aaaUse .NET Core tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konuda nasıl toouse .NET toocreate tooan Azure SQL veritabanına bağlanan bir program çekirdek ve Transact-SQL deyimi kullanarak sorgu gösterilmektedir."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="d326f-103">.NET Core (C#) tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="d326f-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="d326f-104">Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [.NET Core](https://www.microsoft.com/net/) Linux/Windows/macOS toocreate C# programı tooconnect tooan üzerinde Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d326f-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d326f-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d326f-105">Prerequisites</span></span>

<span data-ttu-id="d326f-106">toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d326f-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="d326f-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d326f-107">An Azure SQL database.</span></span> <span data-ttu-id="d326f-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="d326f-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="d326f-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="d326f-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="d326f-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="d326f-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="d326f-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d326f-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="d326f-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d326f-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="d326f-113">[İşletim sisteminiz için .NET Core](https://www.microsoft.com/net/core) yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="d326f-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="d326f-114">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="d326f-114">SQL server connection information</span></span>

<span data-ttu-id="d326f-115">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="d326f-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="d326f-116">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="d326f-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="d326f-117">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d326f-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d326f-118">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d326f-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="d326f-119">Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş.</span><span class="sxs-lookup"><span data-stu-id="d326f-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="d326f-120">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d326f-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="d326f-122">Azure SQL veritabanı sunucusu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin.</span><span class="sxs-lookup"><span data-stu-id="d326f-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="d326f-123">Gerekirse, hello parolayı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d326f-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="d326f-124">**Veritabanı bağlantı dizelerini göster**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d326f-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="d326f-125">Gözden geçirme hello tam **ADO.NET** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="d326f-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesi](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="d326f-127">Bu öğreticiyi gerçekleştirme hello bilgisayarın hello ortak IP adresi için yerinde bir güvenlik duvarı kuralı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d326f-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="d326f-128">Farklı bir bilgisayarda olan veya farklı bir ortak IP adresi varsa, oluşturma bir [sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="d326f-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="d326f-129">Yeni bir .NET projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d326f-129">Create a new .NET project</span></span>

1. <span data-ttu-id="d326f-130">Komut istemini açın ve *sqltest* adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d326f-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="d326f-131">Oluşturulan ve hello aşağıdaki komutu çalıştırın toohello klasörüne gidin:</span><span class="sxs-lookup"><span data-stu-id="d326f-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="d326f-132">Açık ***sqltest.csproj*** , sık kullandığınız metin düzenleyicisinde ve System.Data.SqlClient koddan hello kullanarak bağımlılık olarak ekleme:</span><span class="sxs-lookup"><span data-stu-id="d326f-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="d326f-133">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="d326f-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="d326f-134">Geliştirme ortamınızda veya sık kullandığınız metin düzenleyicisinde **Program.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d326f-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="d326f-135">Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d326f-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="d326f-136">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d326f-136">Run hello code</span></span>

1. <span data-ttu-id="d326f-137">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d326f-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="d326f-138">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d326f-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d326f-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d326f-139">Next steps</span></span>

- <span data-ttu-id="d326f-140">[Windows/Linux/macOS hello komut satırını kullanarak .NET Çekirdeğinde ile çalışmaya başlama](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="d326f-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="d326f-141">Nasıl çok öğrenin[bağlanma ve hello .NET framework ve Visual Studio kullanarak Azure SQL veritabanını sorgulama](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="d326f-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="d326f-142">Nasıl çok öğrenin[SSMS kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database.md) veya [.NET kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="d326f-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="d326f-143">.NET hakkında daha fazla bilgi edinmek için [.NET belgelerine](https://docs.microsoft.com/dotnet/) bakın.</span><span class="sxs-lookup"><span data-stu-id="d326f-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
