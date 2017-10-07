---
title: "aaaUse Node.js tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Node.js toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="c82f8-103">Node.js tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="c82f8-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="c82f8-104">Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [Node.js](https://nodejs.org/en/) toocreate program tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c82f8-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c82f8-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c82f8-105">Prerequisites</span></span>

<span data-ttu-id="c82f8-106">toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="c82f8-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="c82f8-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c82f8-107">An Azure SQL database.</span></span> <span data-ttu-id="c82f8-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="c82f8-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="c82f8-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="c82f8-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="c82f8-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="c82f8-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="c82f8-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c82f8-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="c82f8-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c82f8-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="c82f8-113">İşletim sisteminiz için Node.js ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="c82f8-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="c82f8-114">**MacOS**: Homebrew ve Node.js ve hello ODBC sürücüsü ve SQLCMD yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c82f8-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="c82f8-115">Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="c82f8-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="c82f8-116">**Ubuntu**: Node.js ve hello ODBC sürücüsü ve SQLCMD yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c82f8-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="c82f8-117">Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="c82f8-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="c82f8-118">**Windows**: Chocolatey ve Node.js ve hello ODBC sürücüsü ve SQL cmd yükleyin</span><span class="sxs-lookup"><span data-stu-id="c82f8-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="c82f8-119">Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="c82f8-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="c82f8-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="c82f8-120">SQL server connection information</span></span>

<span data-ttu-id="c82f8-121">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="c82f8-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="c82f8-122">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="c82f8-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="c82f8-123">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c82f8-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c82f8-124">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c82f8-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="c82f8-125">Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş.</span><span class="sxs-lookup"><span data-stu-id="c82f8-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="c82f8-126">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c82f8-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="c82f8-128">Merhaba oturum açma bilgilerini Azure SQL veritabanı sunucunuz için unuttuysanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.</span><span class="sxs-lookup"><span data-stu-id="c82f8-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c82f8-129">Bu öğreticiyi gerçekleştirme hello bilgisayarın hello ortak IP adresi için yerinde bir güvenlik duvarı kuralı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c82f8-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="c82f8-130">Farklı bir bilgisayarda olan veya farklı bir ortak IP adresi varsa, oluşturma bir [sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="c82f8-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="c82f8-131">Node.js projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c82f8-131">Create a Node.js project</span></span>

<span data-ttu-id="c82f8-132">Komut istemini açın ve *sqltest* adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c82f8-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="c82f8-133">Oluşturulan ve hello aşağıdaki komutu çalıştırın toohello klasörüne gidin:</span><span class="sxs-lookup"><span data-stu-id="c82f8-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="c82f8-134">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="c82f8-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="c82f8-135">Geliştirme ortamınızda veya sık kullandığınız metin düzenleyicisinde **sqltest.js** adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c82f8-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="c82f8-136">Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c82f8-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a><span data-ttu-id="c82f8-137">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c82f8-137">Run hello code</span></span>

1. <span data-ttu-id="c82f8-138">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c82f8-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="c82f8-139">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c82f8-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c82f8-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c82f8-140">Next steps</span></span>

- <span data-ttu-id="c82f8-141">Merhaba hakkında bilgi edinin [SQL Server için Microsoft Node.js Driver](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="c82f8-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="c82f8-142">Nasıl çok öğrenin[bağlanma ve .NET core kullanarak Azure SQL veritabanını sorgulama](sql-database-connect-query-dotnet-core.md) Linux/Windows/macOS üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c82f8-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="c82f8-143">Hakkında bilgi edinin [Windows/Linux/macOS hello komut satırını kullanarak .NET Çekirdeğinde ile çalışmaya başlama](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c82f8-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="c82f8-144">Nasıl çok öğrenin[SSMS kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database.md) veya [.NET kullanarak ilk Azure SQL veritabanınızı tasarım](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c82f8-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="c82f8-145">Nasıl çok öğrenin[bağlanma ve sorgu SSMS ile](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="c82f8-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="c82f8-146">Nasıl çok öğrenin[bağlanma ve sorgu Visual Studio Code ile](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="c82f8-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


