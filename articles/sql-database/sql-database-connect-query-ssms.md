---
title: "SSMS: Azure SQL Veritabanında verileri bağlama ve sorgulama | Microsoft Docs"
description: "Bilgi nasıl tooconnect tooSQL veritabanına Azure üzerinde SQL Server Management Studio (SSMS) kullanarak. Ardından, Transact-SQL (T-SQL) deyimleri tooquery ve düzenleme veri çalıştırın."
metacanonical: 
keywords: "bağlantı toosql veritabanı, sql server management Studio'da"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="8ece8-105">Azure SQL veritabanı: SQL Server Management Studio'yu kullanın tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="8ece8-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="8ece8-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) olan herhangi bir SQL altyapı veritabanı Windows için Microsoft SQL Server tooSQL yönetme için tümleşik bir ortam.</span><span class="sxs-lookup"><span data-stu-id="8ece8-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="8ece8-107">Bu hızlı başlangıç nasıl toouse SSMS tooconnect tooan Azure SQL veritabanı ve kullanım Transact-SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ece8-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8ece8-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8ece8-108">Prerequisites</span></span>

<span data-ttu-id="8ece8-109">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan başlangıç noktası hello kaynaklarını kullanır:</span><span class="sxs-lookup"><span data-stu-id="8ece8-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="8ece8-110">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="8ece8-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="8ece8-111">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="8ece8-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="8ece8-112">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ece8-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="8ece8-113">Başlamadan önce hello en yeni sürümünü yüklediğinizden emin olun [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ece8-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="8ece8-114">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="8ece8-114">SQL server connection information</span></span>

<span data-ttu-id="8ece8-115">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="8ece8-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8ece8-116">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ece8-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8ece8-117">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ece8-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8ece8-118">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="8ece8-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8ece8-119">Merhaba üzerinde **genel bakış** sayfasında veritabanınız için hello resimde gösterildiği gibi hello tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8ece8-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="8ece8-120">Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="8ece8-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![bağlantı bilgileri](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8ece8-122">Merhaba oturum açma bilgilerini Azure SQL veritabanı sunucunuz için unuttuysanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.</span><span class="sxs-lookup"><span data-stu-id="8ece8-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="8ece8-123">Tooyour veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="8ece8-123">Connect tooyour database</span></span>

<span data-ttu-id="8ece8-124">SQL Server Management Studio tooestablish bağlantı tooyour Azure SQL veritabanı sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ece8-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8ece8-125">Azure SQL Veritabanı mantıksal sunucusu 1433 numaralı bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="8ece8-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="8ece8-126">Tooconnect tooan Azure SQL Database mantıksal sunucudan kurumsal bir güvenlik duvarı içinde çalışıyorsanız, toosuccessfully bağlanmak için bu bağlantı noktası hello Kurumsal Güvenlik Duvarı'nda açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ece8-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="8ece8-127">SQL Server Management Studio’yu açın.</span><span class="sxs-lookup"><span data-stu-id="8ece8-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="8ece8-128">Merhaba, **tooServer bağlanmak** iletişim kutusunda, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="8ece8-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="8ece8-129">Ayar</span><span class="sxs-lookup"><span data-stu-id="8ece8-129">Setting</span></span>       | <span data-ttu-id="8ece8-130">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="8ece8-130">Suggested value</span></span> | <span data-ttu-id="8ece8-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ece8-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="8ece8-132">**Sunucu türü**</span><span class="sxs-lookup"><span data-stu-id="8ece8-132">**Server type**</span></span> | <span data-ttu-id="8ece8-133">Veritabanı altyapısı</span><span class="sxs-lookup"><span data-stu-id="8ece8-133">Database engine</span></span> | <span data-ttu-id="8ece8-134">Bu değer gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8ece8-134">This value is required.</span></span> |
   | <span data-ttu-id="8ece8-135">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="8ece8-135">**Server name**</span></span> | <span data-ttu-id="8ece8-136">Merhaba tam sunucu adı</span><span class="sxs-lookup"><span data-stu-id="8ece8-136">hello fully qualified server name</span></span> | <span data-ttu-id="8ece8-137">Merhaba adı şöyle olmalıdır: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="8ece8-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="8ece8-138">**Kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="8ece8-138">**Authentication**</span></span> | <span data-ttu-id="8ece8-139">SQL Server Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8ece8-139">SQL Server Authentication</span></span> | <span data-ttu-id="8ece8-140">SQL kimlik doğrulaması biz Bu öğreticide yapılandırdığınız hello yalnızca kimlik doğrulaması türüdür.</span><span class="sxs-lookup"><span data-stu-id="8ece8-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="8ece8-141">**Oturum açma**</span><span class="sxs-lookup"><span data-stu-id="8ece8-141">**Login**</span></span> | <span data-ttu-id="8ece8-142">Merhaba server yönetici hesabı</span><span class="sxs-lookup"><span data-stu-id="8ece8-142">hello server admin account</span></span> | <span data-ttu-id="8ece8-143">Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="8ece8-144">**Parola**</span><span class="sxs-lookup"><span data-stu-id="8ece8-144">**Password**</span></span> | <span data-ttu-id="8ece8-145">Sunucu yönetici hesabınız için Hello parola</span><span class="sxs-lookup"><span data-stu-id="8ece8-145">hello password for your server admin account</span></span> | <span data-ttu-id="8ece8-146">Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello paroladır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-146">This is hello password that you specified when you created hello server.</span></span> |

   ![tooserver Bağlan](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="8ece8-148">Tıklatın **seçenekleri** hello içinde **tooserver bağlanmak** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="8ece8-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="8ece8-149">Merhaba, **toodatabase bağlanmak** bölümünde, girin **mySampleDatabase** tooconnect toothis veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8ece8-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![sunucuda toodb Bağlan](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="8ece8-151">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ece8-151">Click **Connect**.</span></span> <span data-ttu-id="8ece8-152">SSMS Hello Nesne Gezgini penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![bağlı tooserver](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="8ece8-154">Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **mySampleDatabase** hello örnek veritabanındaki tooview hello nesneleri.</span><span class="sxs-lookup"><span data-stu-id="8ece8-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="8ece8-155">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="8ece8-155">Query data</span></span>

<span data-ttu-id="8ece8-156">Kullanım hello aşağıdaki kod tooquery hello ilk 20 ürünleri için hello kullanarak kategoriye göre [seçin](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="8ece8-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8ece8-157">Nesne Gezgini’nde **mySampleDatabase** öğesine sağ tıklayıp **Yeni Sorgu**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ece8-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="8ece8-158">Boş sorgu penceresi bağlı tooyour veritabanını başka bir deyişle açar.</span><span class="sxs-lookup"><span data-stu-id="8ece8-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="8ece8-159">Merhaba sorgu penceresinde, sorgu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="8ece8-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="8ece8-160">Merhaba araç çubuğundan, **yürütme** hello ürün ve ProductCategory tablolarındaki tooretrieve verileri.</span><span class="sxs-lookup"><span data-stu-id="8ece8-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![sorgu](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="8ece8-162">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="8ece8-162">Insert data</span></span>

<span data-ttu-id="8ece8-163">Kullanım hello aşağıdaki hello SalesLT.Product tabloya hello kullanarak yeni bir ürün tooinsert kod [Ekle](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="8ece8-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8ece8-164">Merhaba sorgu penceresinde hello önceki sorgu sorgu aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="8ece8-164">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="8ece8-165">Merhaba araç çubuğundan, **yürütme** tooinsert hello ürün tablosunda yeni bir satır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="8ece8-166">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="8ece8-166">Update data</span></span>

<span data-ttu-id="8ece8-167">Kullanım hello aşağıdaki kod tooupdate hello yeni ürün hello kullanarak daha önce eklediğiniz [güncelleştirme](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="8ece8-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8ece8-168">Merhaba sorgu penceresinde hello önceki sorgu sorgu aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="8ece8-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="8ece8-169">Merhaba araç çubuğundan, **yürütme** hello ürün tablosundaki tooupdate hello belirtilen satır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="8ece8-170">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="8ece8-170">Delete data</span></span>

<span data-ttu-id="8ece8-171">Kullanım hello aşağıdaki kod toodelete hello yeni ürün hello kullanarak daha önce eklediğiniz [silmek](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="8ece8-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8ece8-172">Merhaba sorgu penceresinde hello önceki sorgu sorgu aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="8ece8-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="8ece8-173">Merhaba araç çubuğundan, **yürütme** hello ürün tablosundaki toodelete hello belirtilen satır.</span><span class="sxs-lookup"><span data-stu-id="8ece8-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="8ece8-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ece8-174">Next steps</span></span>

- <span data-ttu-id="8ece8-175">sunucular ve veritabanları Transact-SQL ile oluşturma ve yönetme hakkında toolearn bkz [Azure SQL veritabanı sunucuları ve veritabanları hakkında daha fazla bilgi](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="8ece8-176">SSMS hakkında bilgi için bkz. [SQL Server Management Studio'yu Kullanma](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ece8-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="8ece8-177">bkz: tooconnect ve Visual Studio Code kullanarak sorgu [bağlanma ve sorgu Visual Studio Code ile](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="8ece8-178">bkz: tooconnect ve .NET kullanarak sorgu [bağlanma ve sorgu .NET ile](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="8ece8-179">bkz: tooconnect ve PHP, kullanarak sorgu [Connect ve PHP sorguyla](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="8ece8-180">bkz: tooconnect ve Node.js kullanarak sorgu [Connect ve Node.js sorguyla](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="8ece8-181">bkz: tooconnect ve Java kullanarak sorgu [Connect ve Java sorguyla](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="8ece8-182">bkz: tooconnect ve Python kullanarak sorgu [Connect ve Python sorguyla](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="8ece8-183">bkz: tooconnect ve Ruby, kullanarak sorgu [Connect ve Ruby sorguyla](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="8ece8-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
