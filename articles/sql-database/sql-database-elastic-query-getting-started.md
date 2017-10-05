---
title: "Rapor (yatay bölümleme) ölçeklendirilmiş bulut veritabanları arasında | Microsoft Docs"
description: "Veritabanı veritabanı sorgularını kullanma"
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
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="dcbe0-103">Ölçeklendirilen bulut veritabanları arasında (Önizleme) raporu</span><span class="sxs-lookup"><span data-stu-id="dcbe0-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="dcbe0-104">Tek bir bağlantı noktası kullanarak birden çok Azure SQL veritabanından raporlar oluşturmak bir [esnek sorgu](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="dcbe0-105">Veritabanlarını yatay (aynı zamanda "parçalı" olarak da bilinir) bölümlenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="dcbe0-106">Var olan bir veritabanı varsa, bkz: [ölçeklendirilmiş veritabanları için var olan veritabanlarını taşıma](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="dcbe0-107">Sorgu için gerekli olan SQL nesneler anlamak için bkz: [sorgu yatay olarak bölümlenmiş veritabanları arasında](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcbe0-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dcbe0-108">Prerequisites</span></span>
<span data-ttu-id="dcbe0-109">İndirme ve çalıştırma [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="dcbe0-110">Harita manager örnek uygulamasını kullanarak bir parça oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcbe0-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="dcbe0-111">Burada birkaç parça parça veri ekleme tarafından izlenen, birlikte Yöneticisi bir parça eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="dcbe0-112">Parçalı veriler parça Kurulumu zaten olması görülüyorsa, aşağıdaki adımları atlayın ve sonraki bölüme taşıyın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="dcbe0-113">Derleme ve çalıştırma **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="dcbe0-114">Adım 7 bölümünde kadar adımları [örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="dcbe0-115">Adım 7 sonunda, aşağıdaki komut istemi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![Komut İstemi][1]
2. <span data-ttu-id="dcbe0-117">Komut penceresinde "1" yazın ve tuşuna basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="dcbe0-118">Bu parça eşleme Yöneticisi oluşturur ve iki parça sunucusuna ekler.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="dcbe0-119">Daha sonra "3" yazın ve basın **Enter**; eylem dört kez yineler.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="dcbe0-120">Bu örnek verileri satır, parça ekler.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="dcbe0-121">[Azure portal](https://portal.azure.com) üç yeni veritabanları sunucunuzun göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio onayı][2]

   <span data-ttu-id="dcbe0-123">Bu noktada, veritabanları arası sorguları esnek veritabanı istemci kitaplıkları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="dcbe0-124">Örneğin, komut penceresinde 4 seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="dcbe0-125">Çok parça sorgusundan gelen sonuçları her zaman olan bir **UNION ALL** tüm parça sonuçları.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="dcbe0-126">Sonraki bölümde, verilerin parça arasında daha zengin sorgulama destekleyen bir örnek veritabanı uç noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="dcbe0-127">Esnek sorgu veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcbe0-127">Create an elastic query database</span></span>
1. <span data-ttu-id="dcbe0-128">Açık [Azure portal](https://portal.azure.com) ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="dcbe0-129">Parça kurulumunuzu aynı sunucuda yeni bir Azure SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="dcbe0-130">"ElasticDBQuery." veritabanı adı</span><span class="sxs-lookup"><span data-stu-id="dcbe0-130">Name the database "ElasticDBQuery."</span></span>

    ![Azure portalı ve fiyatlandırma katmanı][3]

    > [!NOTE]
    > <span data-ttu-id="dcbe0-132">Varolan bir veritabanını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-132">you can use an existing database.</span></span> <span data-ttu-id="dcbe0-133">Bunu yapmak, sorgularınızı yürütmek istediğiniz parça birini olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="dcbe0-134">Bu veritabanı, esnek veritabanı sorgusu için meta veri nesnesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="dcbe0-135">Veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcbe0-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="dcbe0-136">Veritabanı kapsamlı ana anahtar ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="dcbe0-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="dcbe0-137">Bunlar, parça parça eşleme Yöneticisi'ni bağlamak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="dcbe0-138">SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="dcbe0-139">ElasticDBQuery veritabanına bağlanmak ve aşağıdaki T-SQL komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="dcbe0-140">"username" ve "parola" olmalıdır yordamının 6. adımında kullanılan oturum açma bilgileri aynı [örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) içinde [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="dcbe0-141">Dış veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="dcbe0-141">External data sources</span></span>
<span data-ttu-id="dcbe0-142">Dış veri kaynağı oluşturmak için ElasticDBQuery veritabanında aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="dcbe0-143">Esnek veritabanı araçlarını örnek kullanarak parça eşleme Yöneticisi ve parça eşleme oluşturduysanız "CustomerIDShardMap" parça eşleme adıdır.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="dcbe0-144">Ancak, bu örnek için özel kurulum kullandıysanız, uygulamanızda seçtiğiniz parça eşleme adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="dcbe0-145">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="dcbe0-145">External tables</span></span>
<span data-ttu-id="dcbe0-146">ElasticDBQuery veritabanı üzerinde şu komutu yürüterek parça Müşteriler tablosunda eşleşen bir dış tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="dcbe0-147">Bir örnek esnek veritabanı T-SQL sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="dcbe0-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="dcbe0-148">Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolar üzerindeki tam T-SQL artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="dcbe0-149">Bu sorgu ElasticDBQuery veritabanında yürütün:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="dcbe0-150">Sorgu sonuçları tüm parça toplar ve aşağıdaki çıkış verir görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="dcbe0-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Çıkış Ayrıntıları][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="dcbe0-152">Esnek veritabanı sorgu sonuçları Excel'e Al</span><span class="sxs-lookup"><span data-stu-id="dcbe0-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="dcbe0-153">Gelen bir sorgunun sonuçlarını bir Excel dosyasını içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="dcbe0-154">Excel 2013'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="dcbe0-155">Gidin **veri** Şerit.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="dcbe0-156">Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel Import diğer kaynaklardan][5]
4. <span data-ttu-id="dcbe0-158">İçinde **Veri Bağlantı Sihirbazı** sunucu adını ve oturum açma kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="dcbe0-159">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-159">Then click **Next**.</span></span>
5. <span data-ttu-id="dcbe0-160">İletişim kutusunda **istediğiniz verileri içeren bir veritabanı seçin**seçin **ElasticDBQuery** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="dcbe0-161">Seçin **müşteriler** Tablo liste görünümünde ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="dcbe0-162">Ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="dcbe0-163">İçinde **veri içeri aktarma** formunda, altında **nasıl çalışma kitabınızı bu verileri görüntülemek istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="dcbe0-164">Tüm satırların **müşteriler** tablo, farklı parça içinde depolanan doldurmak Excel sayfası.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="dcbe0-165">Şimdi, Excel'in güçlü veri görselleştirme işlevlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="dcbe0-166">BI ve veri tümleştirme araçlarınızı esnek sorgu veritabanına bağlanmak için sunucu adını, veritabanı adının ve kimlik bilgileri ile bağlantı dizesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="dcbe0-167">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="dcbe0-168">Herhangi bir SQL Server veritabanı gibi dış tablolar ve aracı ile bağlanacağı SQL Server tablolarını ve esnek sorgu veritabanı başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="dcbe0-169">Maliyet</span><span class="sxs-lookup"><span data-stu-id="dcbe0-169">Cost</span></span>
<span data-ttu-id="dcbe0-170">Esnek veritabanı sorgusu özelliğini kullanmak için ek ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="dcbe0-171">Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcbe0-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dcbe0-172">Next steps</span></span>

* <span data-ttu-id="dcbe0-173">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="dcbe0-174">Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe0-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="dcbe0-175">Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="dcbe0-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="dcbe0-176">Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="dcbe0-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="dcbe0-177">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="dcbe0-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
