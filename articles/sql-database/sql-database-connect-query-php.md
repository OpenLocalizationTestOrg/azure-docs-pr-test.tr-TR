---
title: "aaaUse PHP tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse PHP toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
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
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="f6dd7-103">PHP tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="f6dd7-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="f6dd7-104">Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate program tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6dd7-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f6dd7-105">Prerequisites</span></span>

<span data-ttu-id="f6dd7-106">toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f6dd7-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="f6dd7-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-107">An Azure SQL database.</span></span> <span data-ttu-id="f6dd7-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="f6dd7-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="f6dd7-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="f6dd7-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="f6dd7-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="f6dd7-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="f6dd7-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6dd7-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="f6dd7-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="f6dd7-113">İşletim sisteminiz için PHP ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="f6dd7-114">**MacOS**: Homebrew yükleyin ve PHP, hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için PHP sürücü hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="f6dd7-115">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="f6dd7-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="f6dd7-116">**Ubuntu**: PHP yüklemek ve diğer SQL Server için gerekli paketleri ve yükleme hello PHP sürücü.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="f6dd7-117">Bkz. [Adım 1.2 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="f6dd7-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="f6dd7-118">**Windows**: hello en yeni sürümünü yüklemek PHP için IIS Express, Microsoft SQL Server için Drivers IIS Express, Chocolatey, hello ODBC sürücüsü ve SQLCMD hello en yeni sürümü.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="f6dd7-119">Bkz. [Adım 1.2 ve 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="f6dd7-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="f6dd7-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="f6dd7-120">SQL server connection information</span></span>

<span data-ttu-id="f6dd7-121">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="f6dd7-122">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="f6dd7-123">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6dd7-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f6dd7-124">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="f6dd7-125">Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="f6dd7-126">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f6dd7-128">Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="f6dd7-129">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="f6dd7-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="f6dd7-130">Sık kullandığınız metin düzenleyicisinde **sqltest.php** adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="f6dd7-131">Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
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

## <a name="run-hello-code"></a><span data-ttu-id="f6dd7-132">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f6dd7-132">Run hello code</span></span>

1. <span data-ttu-id="f6dd7-133">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f6dd7-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="f6dd7-134">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f6dd7-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6dd7-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6dd7-135">Next steps</span></span>
- [<span data-ttu-id="f6dd7-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="f6dd7-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="f6dd7-137">SQL Server için Microsoft PHP Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="f6dd7-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="f6dd7-138">Sorun bildirin veya soru sorun</span><span class="sxs-lookup"><span data-stu-id="f6dd7-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
