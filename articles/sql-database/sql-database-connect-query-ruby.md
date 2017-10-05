---
title: "Azure SQL Veritabanı sorgulamak için Ruby kullanma | Microsoft Docs"
description: "Bu konu başlığı altında, Ruby kullanarak Azure SQL Veritabanına bağlanan ve Transact-SQL deyimleriyle veritabanını sorgulayan bir program oluşturma işlemi gösterilir."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="447a2-103">Ruby kullanarak Azure SQL veritabanı sorgulama</span><span class="sxs-lookup"><span data-stu-id="447a2-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="447a2-104">Bu hızlı başlangıç öğreticisi, [Ruby](https://www.ruby-lang.org) kullanarak Azure SQL veritabanına bağlanan ve Transact-SQL deyimleriyle veri sorgulayan bir program oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="447a2-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="447a2-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="447a2-105">Prerequisites</span></span>

<span data-ttu-id="447a2-106">Bu hızlı başlangıç öğreticisini tamamlamak için aşağıdaki önkoşulların karşılandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="447a2-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="447a2-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="447a2-107">An Azure SQL database.</span></span> <span data-ttu-id="447a2-108">Bu hızlı başlangıçta, aşağıdaki hızlı başlangıçlardan birinde oluşturulan kaynaklar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="447a2-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="447a2-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="447a2-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="447a2-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="447a2-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="447a2-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="447a2-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="447a2-112">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için [sunucu düzeyinde bir güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="447a2-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="447a2-113">İşletim sisteminiz için Ruby ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="447a2-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="447a2-114">**MacOS**: Homebrew'i, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="447a2-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="447a2-115">Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="447a2-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="447a2-116">**Ubuntu**: Ruby'nin önkoşullarını yükleyin, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="447a2-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="447a2-117">Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="447a2-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="447a2-118">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="447a2-118">SQL server connection information</span></span>

<span data-ttu-id="447a2-119">Azure SQL veritabanına bağlanmak için gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="447a2-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="447a2-120">Sonraki yordamlarda tam sunucu adına, veritabanı adına ve oturum açma bilgilerine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="447a2-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="447a2-121">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="447a2-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="447a2-122">Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="447a2-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="447a2-123">Veritabanınızın **Genel Bakış** sayfasında, tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="447a2-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="447a2-124">Aşağıdaki resimde gösterildiği gibi, sunucu adının üzerine gelerek **Kopyalamak için tıklayın** seçeneğini ortaya çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="447a2-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="447a2-126">Azure SQL Veritabanı sunucunuzun oturum açma bilgilerini unuttuysanız, SQL Veritabanı sunucu sayfasına giderek sunucu yöneticisi adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="447a2-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="447a2-127">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için bir güvenlik duvarı kuralınız olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="447a2-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="447a2-128">Farklı bir bilgisayar kullanıyorsanız veya farklı bir genel IP adresiniz varsa [Azure portal kullanarak bir sunucu düzeyi güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="447a2-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="447a2-129">SQL veritabanını sorgulamak için kod girme</span><span class="sxs-lookup"><span data-stu-id="447a2-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="447a2-130">Sık kullandığınız metin düzenleyicisinde **sqltest.rb** adında yeni bir dosya oluşturun</span><span class="sxs-lookup"><span data-stu-id="447a2-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="447a2-131">İçeriğini aşağıdaki kod ile değiştirin ve sunucunuz, veritabanınız, kullanıcınız ve parolanız için uygun değerleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="447a2-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-the-code"></a><span data-ttu-id="447a2-132">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="447a2-132">Run the code</span></span>

1. <span data-ttu-id="447a2-133">Komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="447a2-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="447a2-134">En üst 20 satırın döndürüldüğünü doğrulayın ve sonra uygulama penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="447a2-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="447a2-135">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="447a2-135">Next Steps</span></span>
- [<span data-ttu-id="447a2-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="447a2-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="447a2-137">TinyTDS için GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="447a2-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="447a2-138">TinyTDS hakkında sorun bildirin veya soru sorun</span><span class="sxs-lookup"><span data-stu-id="447a2-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="447a2-139">SQL Server için Ruby Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="447a2-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
