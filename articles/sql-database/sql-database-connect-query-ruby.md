---
title: "aaaUse Söyleniş tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Söyleniş toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
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
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="f1787-103">Söyleniş tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="f1787-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="f1787-104">Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [Ruby](https://www.ruby-lang.org) toocreate program tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f1787-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1787-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f1787-105">Prerequisites</span></span>

<span data-ttu-id="f1787-106">toocomplete Bu hızlı başlangıç Öğreticisi, Önkoşullar aşağıdaki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f1787-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="f1787-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f1787-107">An Azure SQL database.</span></span> <span data-ttu-id="f1787-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="f1787-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="f1787-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="f1787-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="f1787-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="f1787-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="f1787-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1787-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="f1787-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f1787-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="f1787-113">İşletim sisteminiz için Ruby ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="f1787-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="f1787-114">**MacOS**: Homebrew'i, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f1787-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="f1787-115">Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="f1787-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="f1787-116">**Ubuntu**: Ruby'nin önkoşullarını yükleyin, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f1787-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="f1787-117">Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="f1787-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="f1787-118">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="f1787-118">SQL server connection information</span></span>

<span data-ttu-id="f1787-119">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="f1787-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="f1787-120">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1787-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="f1787-121">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1787-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f1787-122">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="f1787-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="f1787-123">Merhaba üzerinde **genel bakış** sayfasında veritabanınız için hello tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f1787-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="f1787-124">Hello sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** hello görüntü aşağıdaki gösterildiği gibi seçeneği:</span><span class="sxs-lookup"><span data-stu-id="f1787-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f1787-126">Merhaba oturum açma bilgilerini Azure SQL veritabanı sunucunuz için unuttuysanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.</span><span class="sxs-lookup"><span data-stu-id="f1787-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1787-127">Bu öğreticiyi gerçekleştirme hello bilgisayarın hello ortak IP adresi için yerinde bir güvenlik duvarı kuralı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1787-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="f1787-128">Farklı bir bilgisayarda olan veya farklı bir ortak IP adresi varsa, oluşturma bir [sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="f1787-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="f1787-129">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="f1787-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="f1787-130">Sık kullandığınız metin düzenleyicisinde **sqltest.rb** adında yeni bir dosya oluşturun</span><span class="sxs-lookup"><span data-stu-id="f1787-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="f1787-131">Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f1787-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="f1787-132">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f1787-132">Run hello code</span></span>

1. <span data-ttu-id="f1787-133">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f1787-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="f1787-134">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f1787-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f1787-135">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f1787-135">Next Steps</span></span>
- [<span data-ttu-id="f1787-136">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="f1787-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="f1787-137">TinyTDS için GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="f1787-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="f1787-138">TinyTDS hakkında sorun bildirin veya soru sorun</span><span class="sxs-lookup"><span data-stu-id="f1787-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="f1787-139">SQL Server için Ruby Sürücüleri</span><span class="sxs-lookup"><span data-stu-id="f1787-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
