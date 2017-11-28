---
title: "Azure SQL Veritabanı sorgulamak için Python kullanma | Microsoft Docs"
description: "Bu konu başlığı altında, Python kullanarak Azure SQL Veritabanına bağlanan ve Transact-SQL deyimleriyle veritabanını sorgulayan bir program oluşturma işlemi gösterilir."
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
ms.openlocfilehash: afffcb9a4938bf97626f182bb4f4d099d807d411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-python-to-query-an-azure-sql-database"></a><span data-ttu-id="9f00e-103">Python kullanarak Azure SQL veritabanı sorgulama</span><span class="sxs-lookup"><span data-stu-id="9f00e-103">Use Python to query an Azure SQL database</span></span>

 <span data-ttu-id="9f00e-104">Bu hızlı başlangıçta [Python](https://python.org) kullanarak bir Azure SQL veritabanına bağlanma ve Transact-SQL deyimleriyle veri sorgulama işlemleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9f00e-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f00e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9f00e-105">Prerequisites</span></span>

<span data-ttu-id="9f00e-106">Bu hızlı başlangıç öğreticisini tamamlamak için aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9f00e-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="9f00e-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="9f00e-107">An Azure SQL database.</span></span> <span data-ttu-id="9f00e-108">Bu hızlı başlangıçta, aşağıdaki hızlı başlangıçlardan birinde oluşturulan kaynaklar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9f00e-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="9f00e-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="9f00e-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="9f00e-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="9f00e-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="9f00e-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f00e-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="9f00e-112">Bu hızlı başlangıç öğreticisinde kullanacağınız bilgisayarın genel IP adresi için [sunucu düzeyinde bir güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="9f00e-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="9f00e-113">İşletim sisteminiz için Python ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="9f00e-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="9f00e-114">**MacOS**: Homebrew ve Python yükleyin, ODBC sürücüsünü ve SQLCMD yükleyin, ardından SQL Server için Python Sürücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f00e-114">**MacOS**: Install Homebrew and Python, install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="9f00e-115">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="9f00e-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="9f00e-116">**Ubuntu**: Python ve diğer gerekli paketleri yükleyin ve ardından SQL Server için Python Sürücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f00e-116">**Ubuntu**:  Install Python and other required packages, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="9f00e-117">Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="9f00e-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="9f00e-118">**Windows**: Python’un en yeni sürümünü (ortam değişkeni artık sizin için yapılandırılmıştır) yükleyin, ODBC sürücüsünü ve SQLCMD’yi yükleyin ve SQL Server için Python Sürücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f00e-118">**Windows**: Install the newest version of Python (environment variable is now configured for you), install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="9f00e-119">Bkz: [1.2, 1.3 ve 2.1 adımları](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="9f00e-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="9f00e-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="9f00e-120">SQL server connection information</span></span>

<span data-ttu-id="9f00e-121">Azure SQL veritabanına bağlanmak için gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="9f00e-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="9f00e-122">Sonraki yordamlarda tam sunucu adına, veritabanı adına ve oturum açma bilgilerine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9f00e-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="9f00e-123">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9f00e-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f00e-124">Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f00e-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="9f00e-125">Veritabanınızın **Genel Bakış** sayfasında, aşağıdaki görüntüde gösterildiği gibi tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9f00e-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="9f00e-126">Sunucu adının üzerine gelerek **Kopyalamak için tıklayın** seçeneğini ortaya çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f00e-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="9f00e-128">Sunucunuzun oturum açma bilgilerini unuttuysanız SQL Veritabanı sunucusu sayfasına giderek sunucu yöneticisi adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="9f00e-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="9f00e-129">SQL veritabanını sorgulamak için kod girme</span><span class="sxs-lookup"><span data-stu-id="9f00e-129">Insert code to query SQL database</span></span> 

1. <span data-ttu-id="9f00e-130">Sık kullandığınız metin düzenleyicisinde **sqltest.py** adında yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f00e-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="9f00e-131">İçeriğini aşağıdaki kod ile değiştirin ve sunucunuz, veritabanınız, kullanıcınız ve parolanız için uygun değerleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9f00e-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="9f00e-132">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9f00e-132">Run the code</span></span>

1. <span data-ttu-id="9f00e-133">Komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9f00e-133">At the command prompt, run the following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="9f00e-134">En üst 20 satırın döndürüldüğünü doğrulayın ve sonra uygulama penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="9f00e-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f00e-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f00e-135">Next steps</span></span>

- [<span data-ttu-id="9f00e-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="9f00e-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="9f00e-137">SQL Server için Microsoft Python Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="9f00e-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="9f00e-138">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="9f00e-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

