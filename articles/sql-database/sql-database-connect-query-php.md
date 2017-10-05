---
title: "Azure SQL Veritabanını sorgulamak için PHP kullanma | Microsoft Docs"
description: "Bu konu başlığı altında, PHP kullanarak Azure SQL Veritabanına bağlanan ve Transact-SQL deyimleriyle veritabanını sorgulayan bir program oluşturma işlemi gösterilir."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="85e69-103">PHP kullanarak Azure SQL veritabanı sorgulama</span><span class="sxs-lookup"><span data-stu-id="85e69-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="85e69-104">Bu hızlı başlangıç öğreticisi, [PHP](http://php.net/manual/en/intro-whatis.php) kullanarak Azure SQL veritabanına bağlanan ve Transact-SQL deyimleriyle veri sorgulayan bir program oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="85e69-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85e69-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85e69-105">Prerequisites</span></span>

<span data-ttu-id="85e69-106">Bu hızlı başlangıç öğreticisini tamamlamak için aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="85e69-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="85e69-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="85e69-107">An Azure SQL database.</span></span> <span data-ttu-id="85e69-108">Bu hızlı başlangıçta, aşağıdaki hızlı başlangıçlardan birinde oluşturulan kaynaklar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="85e69-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="85e69-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="85e69-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="85e69-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="85e69-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="85e69-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="85e69-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="85e69-112">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için [sunucu düzeyinde bir güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="85e69-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="85e69-113">İşletim sisteminiz için PHP ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="85e69-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="85e69-114">**MacOS**: Homebrew ve PHP yükleyin, ODBC sürücüsünü ve SQLCMD yükleyin, ardından SQL Server için PHP Sürücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="85e69-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="85e69-115">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="85e69-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="85e69-116">**Ubuntu**:  PHP ve diğer gerekli paketleri yükleyin ve ardından SQL Server için PHP Sürücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="85e69-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="85e69-117">Bkz. [Adım 1.2 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="85e69-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="85e69-118">**Windows**: IIS Express için PHP’nin en yeni sürümünü, IIS Express’te SQL Server için Microsoft Sürücülerinin en yeni sürümlerini, Chocolatey, ODBC sürücüsü ve SQLCMD’yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="85e69-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="85e69-119">Bkz. [Adım 1.2 ve 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="85e69-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="85e69-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="85e69-120">SQL server connection information</span></span>

<span data-ttu-id="85e69-121">Azure SQL veritabanına bağlanmak için gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="85e69-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="85e69-122">Sonraki yordamlarda tam sunucu adına, veritabanı adına ve oturum açma bilgilerine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="85e69-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="85e69-123">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="85e69-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="85e69-124">Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85e69-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="85e69-125">Veritabanınızın **Genel Bakış** sayfasında, aşağıdaki görüntüde gösterildiği gibi tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="85e69-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="85e69-126">Sunucu adının üzerine gelerek **Kopyalamak için tıklayın** seçeneğini ortaya çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85e69-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="85e69-128">Sunucunuzun oturum açma bilgilerini unuttuysanız SQL Veritabanı sunucusu sayfasına giderek sunucu yöneticisi adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="85e69-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="85e69-129">SQL veritabanını sorgulamak için kod girme</span><span class="sxs-lookup"><span data-stu-id="85e69-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="85e69-130">Sık kullandığınız metin düzenleyicisinde **sqltest.php** adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85e69-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="85e69-131">İçeriğini aşağıdaki kod ile değiştirin ve sunucunuz, veritabanınız, kullanıcınız ve parolanız için uygun değerleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85e69-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-the-code"></a><span data-ttu-id="85e69-132">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="85e69-132">Run the code</span></span>

1. <span data-ttu-id="85e69-133">Komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85e69-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="85e69-134">En üst 20 satırın döndürüldüğünü doğrulayın ve sonra uygulama penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="85e69-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85e69-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85e69-135">Next steps</span></span>
- [<span data-ttu-id="85e69-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="85e69-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="85e69-137">SQL Server için Microsoft PHP Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="85e69-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="85e69-138">Sorun bildirin veya soru sorun</span><span class="sxs-lookup"><span data-stu-id="85e69-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
