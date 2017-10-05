---
title: "Azure SQL Veritabanı’nı sorgulamak için Visual Studio ve .NET kullanma | Microsoft Docs"
description: "Bu konu başlığı altında, Visual Studio kullanarak Azure SQL Veritabanına bağlanan ve Transact-SQL deyimleriyle veritabanını sorgulayan bir program oluşturma işlemi gösterilir."
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
ms.openlocfilehash: 105dab17823a7e7f6957a604833f4ecad35c14bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-c-with-visual-studio-to-connect-and-query-an-azure-sql-database"></a><span data-ttu-id="c68bf-103">Visual Studio ile .NET (C#) kullanarak Azure SQL veritabanına bağlanma ve veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="c68bf-103">Use .NET (C#) with Visual Studio to connect and query an Azure SQL database</span></span>

<span data-ttu-id="c68bf-104">Bu hızlı başlangıç öğreticisi, [.NET framework](https://www.microsoft.com/net/) kullanarak Visual Studio ile Azure SQL veritabanına bağlanan ve Transact-SQL deyimleriyle veri sorgulayan bir C# programı oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c68bf-104">This quick start tutorial demonstrates how to use the [.NET framework](https://www.microsoft.com/net/) to create a C# program with Visual Studio to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c68bf-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c68bf-105">Prerequisites</span></span>

<span data-ttu-id="c68bf-106">Bu hızlı başlangıç öğreticisini tamamlamak için aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="c68bf-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="c68bf-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c68bf-107">An Azure SQL database.</span></span> <span data-ttu-id="c68bf-108">Bu hızlı başlangıçta, aşağıdaki hızlı başlangıçlardan birinde oluşturulan kaynaklar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c68bf-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="c68bf-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="c68bf-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="c68bf-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="c68bf-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="c68bf-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c68bf-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="c68bf-112">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için [sunucu düzeyinde bir güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="c68bf-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="c68bf-113">[Visual Studio Community 2017, Visual Studio Professional 2017 veya Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="c68bf-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="c68bf-114">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="c68bf-114">SQL server connection information</span></span>

<span data-ttu-id="c68bf-115">Azure SQL veritabanına bağlanmak için gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="c68bf-116">Sonraki yordamlarda tam sunucu adına, veritabanı adına ve oturum açma bilgilerine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c68bf-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="c68bf-117">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c68bf-118">Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="c68bf-119">Veritabanınızın **Genel Bakış** sayfasında, aşağıdaki görüntüde gösterildiği gibi tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="c68bf-120">Sunucu adının üzerine gelerek **Kopyalamak için tıklayın** seçeneğini ortaya çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c68bf-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="c68bf-122">Azure SQL Veritabanı sunucunuzun oturum açma bilgilerini unuttuysanız, SQL Veritabanı sunucu sayfasına giderek sunucu yöneticisi adını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="c68bf-123">Gerekirse parolayı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c68bf-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="c68bf-124">**Veritabanı bağlantı dizelerini göster**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="c68bf-125">Tam **ADO.NET** bağlantı dizesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-125">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesi](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="c68bf-127">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için bir güvenlik duvarı kuralınız olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c68bf-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="c68bf-128">Farklı bir bilgisayar kullanıyorsanız veya farklı bir genel IP adresiniz varsa [Azure portal kullanarak bir sunucu düzeyi güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c68bf-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="c68bf-129">Yeni Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c68bf-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="c68bf-130">Visual Studio'da **Dosya**, **Yeni**, **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="c68bf-131">**Yeni Proje** iletişim kutusunda **Visual C#** öğesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-131">In the **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="c68bf-132">**Konsol Uygulaması**’nı seçin ve projenin adı için *sqltest* girin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-132">Select **Console App** and enter *sqltest* for the project name.</span></span>
4. <span data-ttu-id="c68bf-133">Visual Studio’da yeni projeyi oluşturmak ve açmak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-133">Click **OK** to create and open the new project in Visual Studio</span></span>
4. <span data-ttu-id="c68bf-134">Çözüm Gezgini'nde, **sqltest**'e sağ tıklayın ve **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="c68bf-135">**Gözat**’ta ```System.Data.SqlClient``` öğesini arayın ve bulduğunuzda seçin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-135">On the **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="c68bf-136">**System.Data.SqlClient** sayfasında **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-136">In the **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="c68bf-137">Yükleme tamamlandığında değişiklikleri gözden geçirin ve **Önizleme** penceresini kapamak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-137">When the install completes, review the changes and then click **OK** to close the **Preview** window.</span></span> 
8. <span data-ttu-id="c68bf-138">**Lisans Kabulü** penceresi gösterilirse **Kabul Ediyorum**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="c68bf-139">SQL veritabanını sorgulamak için kod girme</span><span class="sxs-lookup"><span data-stu-id="c68bf-139">Insert code to query SQL database</span></span>
1. <span data-ttu-id="c68bf-140">**Program.cs**’ye geçin (veya gerekiyorsa açın)</span><span class="sxs-lookup"><span data-stu-id="c68bf-140">Switch to (or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="c68bf-141">**Program.cs** dosyasının içeriğini aşağıdaki kodla değiştirin ve sunucunuz, veritabanınız, kullanıcınız ve parolanız için uygun değerleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-141">Replace the contents of **Program.cs** with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="c68bf-142">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c68bf-142">Run the code</span></span>

1. <span data-ttu-id="c68bf-143">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-143">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c68bf-144">En üst 20 satırın döndürüldüğünü doğrulayın ve sonra uygulama penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-144">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c68bf-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c68bf-145">Next steps</span></span>

- <span data-ttu-id="c68bf-146">Windows/Linus/macOS’ta [.NET Core kullanarak Azure SQL veritabanını bağlamayı ve sorgulamayı](sql-database-connect-query-dotnet-core.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-146">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="c68bf-147">[Komut satırını kullanarak Windows/Linus/macOS’ta .NET Core ile çalışmaya başlama](/dotnet/core/tutorials/using-with-xplat-cli) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="c68bf-148">[SSMS kullanarak ilk Azure SQL veritabanınızı tasarlamayı](sql-database-design-first-database.md) veya [.NET kullanarak ilk Azure SQL veritabanınızı tasarlamayı](sql-database-design-first-database-csharp.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c68bf-148">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="c68bf-149">.NET hakkında daha fazla bilgi edinmek için [.NET belgelerine](https://docs.microsoft.com/dotnet/) bakın.</span><span class="sxs-lookup"><span data-stu-id="c68bf-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
