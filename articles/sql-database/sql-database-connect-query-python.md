---
title: "aaaUse Python tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Python toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="acebe-103">Python tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="acebe-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="acebe-104">Bu hızlı başlangıç gösteren nasıl toouse [Python](https://python.org) tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="acebe-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acebe-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="acebe-105">Prerequisites</span></span>

<span data-ttu-id="acebe-106">toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="acebe-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="acebe-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="acebe-107">An Azure SQL database.</span></span> <span data-ttu-id="acebe-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="acebe-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="acebe-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="acebe-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="acebe-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="acebe-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="acebe-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="acebe-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="acebe-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="acebe-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="acebe-113">İşletim sisteminiz için Python ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="acebe-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="acebe-114">**MacOS**: Homebrew yükleyin ve Python hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için hello Python sürücü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="acebe-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="acebe-115">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="acebe-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="acebe-116">**Ubuntu**: Python yüklemek ve diğer SQL Server için gerekli paketleri ve yükleme hello Python sürücü.</span><span class="sxs-lookup"><span data-stu-id="acebe-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="acebe-117">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="acebe-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="acebe-118">**Windows**: hello (ortam değişkeni yapılandırılmış sizin için) Python en yeni sürümünü yüklemek için hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için hello Python sürücü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="acebe-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="acebe-119">Bkz: [1.2, 1.3 ve 2.1 adımları](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="acebe-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="acebe-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="acebe-120">SQL server connection information</span></span>

<span data-ttu-id="acebe-121">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="acebe-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="acebe-122">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="acebe-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="acebe-123">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="acebe-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="acebe-124">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="acebe-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="acebe-125">Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş.</span><span class="sxs-lookup"><span data-stu-id="acebe-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="acebe-126">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="acebe-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="acebe-128">Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.</span><span class="sxs-lookup"><span data-stu-id="acebe-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="acebe-129">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="acebe-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="acebe-130">Sık kullandığınız metin düzenleyicisinde **sqltest.py** adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acebe-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="acebe-131">Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="acebe-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="acebe-132">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="acebe-132">Run hello code</span></span>

1. <span data-ttu-id="acebe-133">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="acebe-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="acebe-134">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="acebe-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acebe-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acebe-135">Next steps</span></span>

- [<span data-ttu-id="acebe-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="acebe-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="acebe-137">SQL Server için Microsoft Python Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="acebe-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="acebe-138">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="acebe-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

