---
title: "ölçeklendirilen bulut veritabanları arasında aaaReporting | Microsoft Docs"
description: "nasıl tooset yatay bölümleri esnek sorguları ayarlama"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="eba2c-103">Raporlama ölçeklendirilmiş bulut veritabanları arasında (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="eba2c-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Parça sorgulama][1]

<span data-ttu-id="eba2c-105">Parçalı veritabanları dağıtmak satırları genişletilmiş bir veri katmanı.</span><span class="sxs-lookup"><span data-stu-id="eba2c-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="eba2c-106">Yatay bölümleme olarak da bilinen tüm katılımcı veritabanlarında Hello şema aynıdır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="eba2c-107">Esnek bir sorgu kullanarak, tüm veritabanları parçalı bir veritabanında span raporlar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba2c-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="eba2c-108">Hızlı Başlangıç için bkz: [ölçeklendirilmiş bulut veritabanları arasında raporlama](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="eba2c-109">Parçalı dışı veritabanları için bkz: [sorgu farklı şemalarda bulut veritabanları arasında](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eba2c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eba2c-110">Prerequisites</span></span>
* <span data-ttu-id="eba2c-111">Merhaba esnek veritabanı istemci kitaplığı kullanılarak bir parça Haritası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eba2c-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="eba2c-112">bkz: [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="eba2c-113">Veya hello örnek uygulamasında kullanma [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="eba2c-114">Alternatif olarak, bkz: [geçirme varolan veritabanları tooscaled kullanıma veritabanları](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="eba2c-115">Merhaba kullanıcı ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="eba2c-116">Bu izni hello ALTER DATABASE iznine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="eba2c-117">ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="eba2c-118">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="eba2c-118">Overview</span></span>
<span data-ttu-id="eba2c-119">Bu deyimler hello meta veri gösterimi parçalı veriler katman hello esnek sorgu veritabanında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eba2c-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="eba2c-120">ANA ANAHTAR OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="eba2c-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="eba2c-121">VERİTABANI KAPSAMLI OLUŞTURMAK KİMLİK BİLGİSİ</span><span class="sxs-lookup"><span data-stu-id="eba2c-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="eba2c-122">DIŞ VERİ KAYNAĞI OLUŞTURUN</span><span class="sxs-lookup"><span data-stu-id="eba2c-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="eba2c-123">DIŞ TABLO OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="eba2c-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="eba2c-124">1.1 kapsamlı veritabanı ana anahtarı ve kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="eba2c-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="eba2c-125">Merhaba kimlik bilgisi hello esnek sorgu tooconnect tooyour Uzak veritabanı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="eba2c-126">Bu hello emin olun *"\<kullanıcıadı\>"* içermez *"@servername"* soneki.</span><span class="sxs-lookup"><span data-stu-id="eba2c-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="eba2c-127">1.2 dış veri kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="eba2c-127">1.2 Create external data sources</span></span>
<span data-ttu-id="eba2c-128">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="eba2c-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="eba2c-129">Örnek</span><span class="sxs-lookup"><span data-stu-id="eba2c-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="eba2c-130">Hello geçerli dış veri kaynaklarının listesini alın:</span><span class="sxs-lookup"><span data-stu-id="eba2c-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="eba2c-131">Parça haritanızı Hello dış veri kaynağına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="eba2c-131">hello external data source references your shard map.</span></span> <span data-ttu-id="eba2c-132">Esnek bir sorgu daha sonra hello dış veri kaynağı ve hello veri katmanındaki katılmak parça eşleme tooenumerate hello veritabanları temel hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="eba2c-133">Merhaba aynı kimlik bilgileri kullanılan tooread hello parça eşleme ve esnek bir sorgu hello işlenmesi sırasında hello parça verileri tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="eba2c-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="eba2c-134">1.3 dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="eba2c-134">1.3 Create external tables</span></span>
<span data-ttu-id="eba2c-135">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="eba2c-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="eba2c-136">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="eba2c-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="eba2c-137">Dış tablolara Hello listesi hello geçerli veritabanından:</span><span class="sxs-lookup"><span data-stu-id="eba2c-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="eba2c-138">toodrop dış tablolar:</span><span class="sxs-lookup"><span data-stu-id="eba2c-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="eba2c-139">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="eba2c-139">Remarks</span></span>
<span data-ttu-id="eba2c-140">Merhaba veri\_SOURCE yan tümcesinde hello dış tablo için kullanılan hello dış veri kaynağı (parça eşleme) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eba2c-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="eba2c-141">Merhaba şema\_adı ve nesne\_adı yan tümceleri hello dış tablo tanımı tooa farklı bir şema tablosunda eşleyin.</span><span class="sxs-lookup"><span data-stu-id="eba2c-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="eba2c-142">Atlanırsa, hello şema hello uzak nesnesinin toobe "dbo" kabul edilir ve adıyla tanımlanan toobe aynı toohello dış tablo adı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="eba2c-143">Bu, uzak tablo hello adını toocreate hello dış tablo istediğiniz hello veritabanında zaten alınmış yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="eba2c-144">Örneğin, bir dış tablo tooget Katalog görünümleri birleşik bir görünümünü toodefine istediğiniz veya genişletilmiş verileriniz üzerinde Dmv'leri katmanı.</span><span class="sxs-lookup"><span data-stu-id="eba2c-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="eba2c-145">Katalog görünümleri ve Dmv'leri zaten yerel olarak mevcut olduğundan, adları hello dış tablo tanımı için kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="eba2c-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="eba2c-146">Bunun yerine, farklı bir ad kullanın ve hello katalog görünümün kullanın veya hello şema DMV'ın adı hello\_adı ve/veya nesne\_adı yan tümceleri.</span><span class="sxs-lookup"><span data-stu-id="eba2c-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="eba2c-147">(Merhaba örneğe bakın.)</span><span class="sxs-lookup"><span data-stu-id="eba2c-147">(See hello example below.)</span></span> 

<span data-ttu-id="eba2c-148">Merhaba dağıtım yan tümcesi Bu tablo için kullanılan hello veri dağılımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="eba2c-149">Merhaba Sorgu işlemcisi hello dağıtım yan tümcesi toobuild hello en verimli sorgu planında sağlanan hello bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="eba2c-150">**PARÇALI** veri hello veritabanları arasında yatay olarak bölümlenmiş anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="eba2c-151">Merhaba veri dağıtım hello için bölümlendirme anahtarı hello **< sharding_column_name >** parametresi.</span><span class="sxs-lookup"><span data-stu-id="eba2c-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="eba2c-152">**ÇOĞALTILAN** özdeş kopyalarını Merhaba tablonun her veritabanını mevcut olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="eba2c-153">Bu, sorumluluk tooensure hello çoğaltmaları hello veritabanları arasında aynı olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="eba2c-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="eba2c-154">**YUVARLAK\_deneme** hello tablosunun yatay olarak bir uygulama bağımlı dağıtım yöntemini kullanılarak bölümlenmiş anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="eba2c-155">**Veri katmanı başvuru**: hello dış tablo DDL tooan dış veri kaynağına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="eba2c-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="eba2c-156">Merhaba dış veri kaynağına hello bilgi gerekli toolocate ile veri katmanındaki tüm hello veritabanları hello dış tablo sağlayan bir parça eşleme belirtir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="eba2c-157">Güvenlikle ilgili dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="eba2c-157">Security considerations</span></span>
<span data-ttu-id="eba2c-158">Erişim toohello dış tablo kullanıcılarla otomatik olarak toohello temel alınan uzak tablolar hello dış veri kaynağı tanımına verilen hello kimlik bilgileri altında erişin.</span><span class="sxs-lookup"><span data-stu-id="eba2c-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="eba2c-159">İstenmeyen ayrıcalıkların hello kimlik bilgisi hello dış veri kaynağının aracılığıyla kaçının.</span><span class="sxs-lookup"><span data-stu-id="eba2c-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="eba2c-160">Yalnızca dizinindeymiş gibi olağan bir tablo için bir dış tablo GRANT veya REVOKE kullanın.</span><span class="sxs-lookup"><span data-stu-id="eba2c-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="eba2c-161">Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra artık dış tablolar üzerindeki tam T-SQL kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba2c-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="eba2c-162">Örnek: yatay bölümlenmiş veritabanlarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="eba2c-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="eba2c-163">Merhaba aşağıdaki sorguyu ambarları, sipariş ve sipariş satırları arasında üç yönlü birleştirme gerçekleştirir ve birkaç toplar ve seçmeli bir filtre kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="eba2c-164">(1) yatay bölümleme (parçalama) ve ambarları, sipariş ve sipariş satırları hello ambar kimliği sütuna göre parçalı ve hello esnek sorgulayan hello birleştirmeler hello parça üzerinde birlikte bulunmasına ve hello pahalı hello hello sorgusunun parçası işleme (2) olduğunu varsayar Paralel parça.</span><span class="sxs-lookup"><span data-stu-id="eba2c-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="eba2c-165">Saklı yordamı uzaktan T-SQL yürütmesi için: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="eba2c-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="eba2c-166">Esnek sorgu aynı zamanda toohello parça doğrudan erişim sağlayan bir saklı yordam sunar.</span><span class="sxs-lookup"><span data-stu-id="eba2c-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="eba2c-167">Merhaba saklı yordam adı verilir [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) ve kullanılan tooexecute uzak saklı yordamları veya T-SQL kodunu hello Uzak veritabanı üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="eba2c-168">Şu parametreler hello alır:</span><span class="sxs-lookup"><span data-stu-id="eba2c-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="eba2c-169">Veri kaynağı adı (nvarchar): hello dış veri kaynağı türü RDBMS hello adı.</span><span class="sxs-lookup"><span data-stu-id="eba2c-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="eba2c-170">Sorgu (nvarchar): hello T-SQL sorgusu toobe her parça üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="eba2c-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="eba2c-171">Parametre bildirimi (nvarchar) - isteğe bağlı: dize veri türü tanımları (gibi sp_executesql) hello Sorgu parametresinde kullanılan hello parametreler için.</span><span class="sxs-lookup"><span data-stu-id="eba2c-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="eba2c-172">Parametre değeri listesi - isteğe bağlı: parametre değerleri (gibi sp_executesql) virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="eba2c-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="eba2c-173">Merhaba sp\_yürütme\_uzak kullanır hello hello çağırma parametreleri tooexecute hello T-SQL deyimini hello uzak veritabanlarında verilen sağlanan dış veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="eba2c-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="eba2c-174">Merhaba dış veri kaynağı tooconnect toohello shardmap manager veritabanı ve hello uzak veritabanlarına hello kimlik bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="eba2c-175">Örnek:</span><span class="sxs-lookup"><span data-stu-id="eba2c-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="eba2c-176">Bağlantı için araçları</span><span class="sxs-lookup"><span data-stu-id="eba2c-176">Connectivity for tools</span></span>
<span data-ttu-id="eba2c-177">Normal SQL Server bağlantı dizelerini tooconnect kullanın, uygulamanızın, BI ve veri tümleştirme araçları toohello veritabanınızla, dış tablo tanımlarını.</span><span class="sxs-lookup"><span data-stu-id="eba2c-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="eba2c-178">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="eba2c-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="eba2c-179">Hello esnek sorgu veritabanını diğer SQL Server veritabanına bağlı toohello araçları gibi başvuru ve yerel tablolar değilmiş gibi aracı veya uygulamadan gelen dış tabloları kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="eba2c-180">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="eba2c-180">Best practices</span></span>
* <span data-ttu-id="eba2c-181">Merhaba esnek sorgu uç veritabanı erişim toohello shardmap veritabanı ve tüm parça hello SQL DB güvenlik duvarları üzerinden verilip verilmediğini emin olun.</span><span class="sxs-lookup"><span data-stu-id="eba2c-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="eba2c-182">Merhaba veri dağıtım hello dış tablo tarafından tanımlanan zorunlu veya doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="eba2c-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="eba2c-183">Gerçek veri dağıtımınız farklıysa, tablo tanımında belirtilen hello dağıtım sorgularınızı beklenmeyen sonuçlar.</span><span class="sxs-lookup"><span data-stu-id="eba2c-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="eba2c-184">Merhaba parçalama anahtarı üzerinden koşulları toosafely dışlama izin verir, esnek sorgu şu anda parça eleme belirli parça işlenmesini gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="eba2c-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="eba2c-185">Esnek sorgu hello hesaplama çoğunu hello parça üzerinde nerede yapılabilir sorguları için en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="eba2c-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="eba2c-186">Genellikle hello en iyi sorgu performansını değerlendirilebilir seçmeli filtre koşulları ile Merhaba parça veya birleştirmeler üzerinde bir bölüme göre hizalı şekilde tüm parça üzerinde gerçekleştirilen anahtarları bölümleme hello üzerinden alırsınız.</span><span class="sxs-lookup"><span data-stu-id="eba2c-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="eba2c-187">Diğer sorgu desenlerine tooload büyük miktarlarda veri hello parça toohello baş düğümünden gerekebilir ve kötü gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="eba2c-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba2c-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eba2c-188">Next steps</span></span>

* <span data-ttu-id="eba2c-189">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="eba2c-190">Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="eba2c-191">Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="eba2c-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="eba2c-192">Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="eba2c-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="eba2c-193">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="eba2c-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
