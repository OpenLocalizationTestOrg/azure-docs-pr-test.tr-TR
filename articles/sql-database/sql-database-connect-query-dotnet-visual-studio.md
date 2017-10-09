---
title: "aaaUse Visual Studio ve .NET tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Visual Studio toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="3565c-103">.NET (C#) ile Visual Studio tooconnect kullanın ve Azure SQL veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="3565c-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="3565c-104">Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate C# programı ile Visual Studio tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3565c-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3565c-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3565c-105">Prerequisites</span></span>

<span data-ttu-id="3565c-106">toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="3565c-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="3565c-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="3565c-107">An Azure SQL database.</span></span> <span data-ttu-id="3565c-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="3565c-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="3565c-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="3565c-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="3565c-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="3565c-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="3565c-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3565c-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="3565c-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3565c-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="3565c-113">[Visual Studio Community 2017, Visual Studio Professional 2017 veya Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="3565c-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="3565c-114">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="3565c-114">SQL server connection information</span></span>

<span data-ttu-id="3565c-115">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="3565c-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="3565c-116">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="3565c-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="3565c-117">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3565c-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3565c-118">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3565c-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3565c-119">Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş.</span><span class="sxs-lookup"><span data-stu-id="3565c-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="3565c-120">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3565c-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3565c-122">Azure SQL veritabanı sunucusu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin.</span><span class="sxs-lookup"><span data-stu-id="3565c-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="3565c-123">Gerekirse, hello parolayı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3565c-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="3565c-124">**Veritabanı bağlantı dizelerini göster**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3565c-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="3565c-125">Gözden geçirme hello tam **ADO.NET** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="3565c-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesi](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="3565c-127">Bu öğreticiyi gerçekleştirme hello bilgisayarın hello ortak IP adresi için yerinde bir güvenlik duvarı kuralı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3565c-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="3565c-128">Farklı bir bilgisayarda olan veya farklı bir ortak IP adresi varsa, oluşturma bir [sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="3565c-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="3565c-129">Yeni Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3565c-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="3565c-130">Visual Studio'da **Dosya**, **Yeni**, **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3565c-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="3565c-131">Merhaba, **yeni proje** iletişim kutusunda ve genişletin **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="3565c-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="3565c-132">Seçin **konsol uygulaması** ve girin *sqltest* hello proje adı.</span><span class="sxs-lookup"><span data-stu-id="3565c-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="3565c-133">Tıklatın **Tamam** toocreate ve açık hello Visual Studio'da yeni proje</span><span class="sxs-lookup"><span data-stu-id="3565c-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="3565c-134">Çözüm Gezgini'nde, **sqltest**'e sağ tıklayın ve **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3565c-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="3565c-135">Merhaba üzerinde **Gözat**, arama ```System.Data.SqlClient``` ve, ne zaman bulunamadı, onu seçin.</span><span class="sxs-lookup"><span data-stu-id="3565c-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="3565c-136">Merhaba, **System.Data.SqlClient** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="3565c-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="3565c-137">Merhaba yükleme tamamlandığında, hello değişiklikleri gözden geçirin ve ardından **Tamam** tooclose hello **Önizleme** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3565c-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="3565c-138">**Lisans Kabulü** penceresi gösterilirse **Kabul Ediyorum**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3565c-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="3565c-139">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="3565c-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="3565c-140">Çok geçiş (veya gerekirse açın) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="3565c-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="3565c-141">Merhaba Değiştir **Program.cs** aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello ile.</span><span class="sxs-lookup"><span data-stu-id="3565c-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="3565c-142">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3565c-142">Run hello code</span></span>

1. <span data-ttu-id="3565c-143">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3565c-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="3565c-144">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3565c-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3565c-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3565c-145">Next steps</span></span>

- <span data-ttu-id="3565c-146">Nasıl çok öğrenin[bağlanma ve .NET core kullanarak Azure SQL veritabanını sorgulama](sql-database-connect-query-dotnet-core.md) Linux/Windows/macOS üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3565c-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="3565c-147">Hakkında bilgi edinin [Windows/Linux/macOS hello komut satırını kullanarak .NET Çekirdeğinde ile çalışmaya başlama](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="3565c-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="3565c-148">Nasıl çok öğrenin[SSMS kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database.md) veya [.NET kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="3565c-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="3565c-149">.NET hakkında daha fazla bilgi edinmek için [.NET belgelerine](https://docs.microsoft.com/dotnet/) bakın.</span><span class="sxs-lookup"><span data-stu-id="3565c-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
