---
title: "(yatay bölümleme) ölçeklendirilmiş bulut veritabanları arasında aaaReport | Microsoft Docs"
description: "nasıl toouse arası veritabanı veritabanı sorguları"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="41924-103">Ölçeklendirilen bulut veritabanları arasında (Önizleme) raporu</span><span class="sxs-lookup"><span data-stu-id="41924-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="41924-104">Tek bir bağlantı noktası kullanarak birden çok Azure SQL veritabanından raporlar oluşturmak bir [esnek sorgu](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41924-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="41924-105">Merhaba veritabanları yatay (aynı zamanda "parçalı" olarak da bilinir) bölümlenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="41924-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="41924-106">Var olan bir veritabanı varsa, bkz: [veritabanları tooscaled kullanıma veritabanlarını taşıma varolan](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="41924-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="41924-107">toounderstand hello SQL nesneleri tooquery gerektiği için bkz: [sorgu yatay olarak bölümlenmiş veritabanları arasında](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="41924-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41924-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41924-108">Prerequisites</span></span>
<span data-ttu-id="41924-109">İndirme ve çalıştırma hello [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41924-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="41924-110">Merhaba örnek uygulaması kullanarak Yöneticisi bir parça eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="41924-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="41924-111">Burada Yöneticisi birlikte hello parça veri ekleme tarafından izlenen birkaç parça parça eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="41924-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="41924-112">Tooalready görülüyorsa parçalı veriler parça Kurulum'a olması, hello aşağıdaki adımları atlayın ve toohello sonraki bölümde taşıyın.</span><span class="sxs-lookup"><span data-stu-id="41924-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="41924-113">Derleme ve çalıştırma hello **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="41924-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="41924-114">Adım 7 hello bölümünde kadar Hello adımları [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="41924-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="41924-115">Adım 7 Hello sonunda, komut istemine aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="41924-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![Komut İstemi][1]
2. <span data-ttu-id="41924-117">Merhaba komut penceresinde "1" yazın ve tuşuna basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="41924-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="41924-118">Bu hello parça eşleme Yöneticisi oluşturur ve iki parça toohello sunucu ekler.</span><span class="sxs-lookup"><span data-stu-id="41924-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="41924-119">Daha sonra "3" yazın ve basın **Enter**; hello eylem dört kez yineler.</span><span class="sxs-lookup"><span data-stu-id="41924-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="41924-120">Bu örnek verileri satır, parça ekler.</span><span class="sxs-lookup"><span data-stu-id="41924-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="41924-121">Merhaba [Azure portal](https://portal.azure.com) üç yeni veritabanları sunucunuzun göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="41924-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio onayı][2]

   <span data-ttu-id="41924-123">Bu noktada, veritabanları arası sorguları hello esnek veritabanı istemci kitaplıkları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="41924-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="41924-124">Örneğin, hello komut penceresinde 4 seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="41924-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="41924-125">bir çok parça sorgudan Hello sonuçlar her zaman bir **UNION ALL** tüm parça hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="41924-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="41924-126">Merhaba sonraki bölümde, daha zengin hello verilerin parça sorgulama destekleyen bir örnek veritabanı uç noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41924-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="41924-127">Esnek sorgu veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41924-127">Create an elastic query database</span></span>
1. <span data-ttu-id="41924-128">Açık hello [Azure portal](https://portal.azure.com) ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="41924-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="41924-129">Hello yeni Azure SQL veritabanı oluşturma parça kurulumunuzu aynı sunucu.</span><span class="sxs-lookup"><span data-stu-id="41924-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="41924-130">Ad hello veritabanını "ElasticDBQuery."</span><span class="sxs-lookup"><span data-stu-id="41924-130">Name hello database "ElasticDBQuery."</span></span>

    ![Azure portalı ve fiyatlandırma katmanı][3]

    > [!NOTE]
    > <span data-ttu-id="41924-132">Varolan bir veritabanını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41924-132">you can use an existing database.</span></span> <span data-ttu-id="41924-133">Bunu yapabilirsiniz tooexecute istediğiniz hello parça biri olması gerekir değil sorgularınızı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="41924-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="41924-134">Bu veritabanı, esnek veritabanı sorgusu için meta veri nesnelerinin hello oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41924-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="41924-135">Veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="41924-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="41924-136">Veritabanı kapsamlı ana anahtar ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="41924-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="41924-137">Kullanılan tooconnect toohello parça eşleme Yöneticisi ve hello parça şunlardır:</span><span class="sxs-lookup"><span data-stu-id="41924-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="41924-138">SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="41924-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="41924-139">TooElasticDBQuery veritabanına bağlanmak ve aşağıdaki T-SQL komutlarıyla hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="41924-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="41924-140">"username" ve "parola" olması hello aynı yordamının 6. adımında kullanılan oturum açma bilgileri olarak [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) içinde [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41924-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="41924-141">Dış veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="41924-141">External data sources</span></span>
<span data-ttu-id="41924-142">bir dış veri kaynağına toocreate komutu hello ElasticDBQuery veritabanında aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="41924-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="41924-143">Merhaba esnek veritabanı araçlarını örneğini kullanarak Yöneticisi hello parça eşleme ve parça eşleme oluşturduysanız "CustomerIDShardMap" Merhaba hello parça eşleme adıdır.</span><span class="sxs-lookup"><span data-stu-id="41924-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="41924-144">Ancak, bu örnek için özel kurulum kullandıysanız, uygulamanızda seçtiğiniz hello parça eşleme adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="41924-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="41924-145">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="41924-145">External tables</span></span>
<span data-ttu-id="41924-146">Komut ElasticDBQuery veritabanında aşağıdaki hello yürüterek hello parça hello Müşteriler tablosunda eşleşen bir dış tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="41924-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="41924-147">Bir örnek esnek veritabanı T-SQL sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="41924-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="41924-148">Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolar üzerindeki tam T-SQL artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41924-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="41924-149">Bu sorgu hello ElasticDBQuery veritabanında yürütün:</span><span class="sxs-lookup"><span data-stu-id="41924-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="41924-150">Merhaba sorgulayan tüm hello parça sonuçları toplar ve çıktı aşağıdaki hello verir görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="41924-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Çıkış Ayrıntıları][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="41924-152">Esnek veritabanı sorgu sonuçları tooExcel alma</span><span class="sxs-lookup"><span data-stu-id="41924-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="41924-153">Merhaba sonuçlarını bir sorgu tooan Excel dosyasını içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41924-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="41924-154">Excel 2013'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="41924-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="41924-155">Toohello gidin **veri** Şerit.</span><span class="sxs-lookup"><span data-stu-id="41924-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="41924-156">Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.</span><span class="sxs-lookup"><span data-stu-id="41924-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel Import diğer kaynaklardan][5]
4. <span data-ttu-id="41924-158">Merhaba, **Veri Bağlantı Sihirbazı** hello sunucu adını ve oturum açma kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="41924-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="41924-159">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41924-159">Then click **Next**.</span></span>
5. <span data-ttu-id="41924-160">Merhaba iletişim kutusunda **hello verileri içeren Select hello veritabanı**seçin hello **ElasticDBQuery** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="41924-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="41924-161">Select hello **müşteriler** tablo hello liste görünümünde ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41924-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="41924-162">Ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="41924-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="41924-163">Merhaba, **veri içeri aktarma** formunda, altında **nasıl bu verileri tooview çalışma kitabınızı istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41924-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="41924-164">Tüm satırları hello **müşteriler** tablo, farklı parça içinde depolanan doldurmak hello Excel sayfası.</span><span class="sxs-lookup"><span data-stu-id="41924-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="41924-165">Şimdi, Excel'in güçlü veri görselleştirme işlevlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41924-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="41924-166">Tooconnect BI ve veri tümleştirme araçları toohello esnek sorgu veritabanınızı kimlik bilgileri ve hello bağlantı dizesi, sunucu adı, veritabanı adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41924-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="41924-167">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="41924-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="41924-168">Toohello esnek sorgu veritabanını ve herhangi bir SQL Server veritabanı gibi dış tablolara ve SQL Server tablolarını aracınızı toowith bağlamak başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="41924-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="41924-169">Maliyet</span><span class="sxs-lookup"><span data-stu-id="41924-169">Cost</span></span>
<span data-ttu-id="41924-170">Merhaba esnek veritabanı sorgusu özelliğini kullanmak için ek ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="41924-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="41924-171">Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="41924-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41924-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41924-172">Next steps</span></span>

* <span data-ttu-id="41924-173">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41924-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="41924-174">Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="41924-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="41924-175">Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="41924-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="41924-176">Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="41924-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="41924-177">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="41924-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
