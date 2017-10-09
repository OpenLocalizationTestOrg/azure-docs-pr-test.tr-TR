---
title: "aaaMigrate varolan veritabanları tooscale kullanıma | Microsoft Docs"
description: "Parça eşleme Yöneticisi oluşturarak parçalı veritabanları toouse esnek veritabanı araçlarını Dönüştür"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="0e099-103">Varolan veritabanları tooscale kullanıma geçirme</span><span class="sxs-lookup"><span data-stu-id="0e099-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="0e099-104">Azure SQL Database veritabanı araçları kullanarak mevcut ölçeklendirilmiş parçalı veritabanlarınız kolayca yönetmenize (Merhaba gibi [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="0e099-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="0e099-105">Var olan bir veritabanları toouse hello dönüştürmeniz gerekir [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="0e099-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0e099-106">Overview</span></span>
<span data-ttu-id="0e099-107">var olan bir parçalı veritabanı toomigrate:</span><span class="sxs-lookup"><span data-stu-id="0e099-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="0e099-108">Merhaba hazırlama [parça eşleme Yöneticisi veritabanı](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="0e099-109">Merhaba parça eşleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e099-109">Create hello shard map.</span></span>
3. <span data-ttu-id="0e099-110">Merhaba tek tek parça hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="0e099-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="0e099-111">Eşlemeleri toohello parça eşleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e099-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="0e099-112">Her iki hello kullanarak bu teknikler uygulanabilir [.NET Framework istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), veya hello PowerShell betikleri bulunması sırasında [Azure SQL veritabanı - esnek veritabanı araçlarını betikleri](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="0e099-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="0e099-113">Burada Hello örnekler hello PowerShell betiklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e099-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="0e099-114">Merhaba ShardMapManager hakkında daha fazla bilgi için bkz: [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="0e099-115">Merhaba esnek veritabanı araçlarını genel bakış için bkz: [esnek veritabanı özelliklere genel bakış](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="0e099-116">Merhaba parça eşleme manager veritabanını hazırlama</span><span class="sxs-lookup"><span data-stu-id="0e099-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="0e099-117">Merhaba parça eşleme Yöneticisi hello veri toomanage ölçeklendirilmiş veritabanlarını içeren özel bir veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="0e099-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="0e099-118">Varolan bir veritabanını kullanın veya yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e099-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="0e099-119">Parça eşleme Yöneticisi hello olmamalıdır bir veritabanı işlevi gören aynı parça veritabanı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e099-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="0e099-120">Ayrıca hello PowerShell Betiği hello veritabanı sizin yerinize oluşturmaz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e099-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="0e099-121">1. adım: bir parça eşleme Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e099-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="0e099-122">tooretrieve hello parça eşleme Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="0e099-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="0e099-123">Oluşturulduktan sonra Bu cmdlet'i hello parça eşleme Yöneticisi alabilir.</span><span class="sxs-lookup"><span data-stu-id="0e099-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="0e099-124">Toouse hello ShardMapManager nesne gereksinim duyduğunuz her zaman bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0e099-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="0e099-125">2. adım: hello parça eşleme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e099-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="0e099-126">Parça eşleme toocreate hello türü seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0e099-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="0e099-127">Merhaba seçim hello veritabanı mimarisine bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="0e099-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="0e099-128">Veritabanı başına tek bir kiracı (Merhaba koşulları için bkz: [sözlüğü](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="0e099-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="0e099-129">Birden çok Kiracı veritabanı (iki tür) başına:</span><span class="sxs-lookup"><span data-stu-id="0e099-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="0e099-130">Liste eşleme</span><span class="sxs-lookup"><span data-stu-id="0e099-130">List mapping</span></span>
   2. <span data-ttu-id="0e099-131">Aralık eşleme</span><span class="sxs-lookup"><span data-stu-id="0e099-131">Range mapping</span></span>

<span data-ttu-id="0e099-132">Tek Kiracı model için oluşturduğunuz bir **listesi eşleme** parça eşleme.</span><span class="sxs-lookup"><span data-stu-id="0e099-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="0e099-133">Merhaba tek kiracılı bir model Kiracı başına tek bir veritabanı atar.</span><span class="sxs-lookup"><span data-stu-id="0e099-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="0e099-134">Yönetimini basitleştirir gibi SaaS geliştiriciler için etkili bir modeli budur.</span><span class="sxs-lookup"><span data-stu-id="0e099-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Liste eşleme][1]

<span data-ttu-id="0e099-136">Merhaba çok kiracılı bir model çeşitli kiracılar tooa tek veritabanı atar (ve kiracılar grupları birden çok veritabanı arasında dağıtabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="0e099-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="0e099-137">Bu model, her Kiracı toohave küçük veri gereken beklediğiniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e099-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="0e099-138">Bu modelde, biz kiracılar tooa veritabanını kullanmanın bir aralığı atamak **aralığı eşleme**.</span><span class="sxs-lookup"><span data-stu-id="0e099-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Aralık eşleme][2]

<span data-ttu-id="0e099-140">Veya, bir çok Kiracı veritabanı modelini kullanarak uygulayabileceğiniz bir *listesi eşleme* tooassign birden çok kiracılar tooa tek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0e099-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="0e099-141">Örneğin, Kiracı kimliği 1 ve 5 kullanılan toostore bilgilerini DB1 olduğu ve DB2 7 Kiracı ve Kiracı 10 için verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="0e099-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Birden fazla kiracılar tek DB][3] 

<span data-ttu-id="0e099-143">**Seçtiğiniz bağlı olarak, aşağıdaki seçeneklerden birini seçin:**</span><span class="sxs-lookup"><span data-stu-id="0e099-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="0e099-144">Seçenek 1: bir liste eşlemesi için bir parça eşleme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e099-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="0e099-145">Merhaba ShardMapManager nesnesi kullanılarak bir parça Haritası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e099-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="0e099-146">Seçenek 2: bir parça eşlemesi için bir aralığı eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e099-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="0e099-147">Bu eşleme deseni bu tooutilize unutmayın, Kiracı kimliği değerleri gereken toobe sürekli aralıkları ve hello veritabanları oluşturulurken hello aralığı yalnızca atlayarak hello aralıklardaki kabul edilebilir toohave boşluk olduğundan.</span><span class="sxs-lookup"><span data-stu-id="0e099-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="0e099-148">Seçenek 3: tek bir veritabanı üzerinde eşlemeleri listesi</span><span class="sxs-lookup"><span data-stu-id="0e099-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="0e099-149">Bu deseni oluşturan ayarı ayrıca bir liste harita oluşturulmasını adım 2, 1. seçenek gösterildiği gibi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e099-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="0e099-150">3. adım: tek tek parça hazırlama</span><span class="sxs-lookup"><span data-stu-id="0e099-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="0e099-151">Her parça (veritabanı) toohello parça eşleme Yöneticisi'ni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e099-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="0e099-152">Bu, hello tek veritabanlarını eşleme bilgilerini depolamak için hazırlar.</span><span class="sxs-lookup"><span data-stu-id="0e099-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="0e099-153">Bu yöntem her parça üzerinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="0e099-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="0e099-154">4. adım: eşlemeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="0e099-154">Step 4: Add mappings</span></span>
<span data-ttu-id="0e099-155">eşlemeleri Hello eklenmesi hello oluşturduğunuz parça eşleme türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0e099-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="0e099-156">Bir liste harita oluşturduysanız, liste eşlemeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e099-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="0e099-157">Bir aralık harita oluşturduysanız, aralık eşlemeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e099-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="0e099-158">Seçenek 1: eşleme hello verilerini listesi eşleme</span><span class="sxs-lookup"><span data-stu-id="0e099-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="0e099-159">Her bir kiracı için bir liste eşlemesi ekleyerek Hello veri eşleme.</span><span class="sxs-lookup"><span data-stu-id="0e099-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="0e099-160">Seçenek 2: eşleme hello veri için bir aralığı eşleme</span><span class="sxs-lookup"><span data-stu-id="0e099-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="0e099-161">Tüm hello Kiracı kimliği aralığı - veritabanı ilişkilendirmeleri Hello aralığı eşlemelerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e099-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="0e099-162">Adım 4 seçenek 3: tek bir veritabanı üzerinde birden çok Kiracı için hello veri eşleme</span><span class="sxs-lookup"><span data-stu-id="0e099-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="0e099-163">Merhaba Ekle ListMapping her bir kiracı için Çalıştır (yukarıda seçenek 1,).</span><span class="sxs-lookup"><span data-stu-id="0e099-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="0e099-164">Merhaba eşlemeleri denetleniyor</span><span class="sxs-lookup"><span data-stu-id="0e099-164">Checking hello mappings</span></span>
<span data-ttu-id="0e099-165">Merhaba varolan parça ve bunlarla ilişkilendirilmiş hello eşlemeleri hakkında bilgi komutları kullanarak sorgulanabilir:</span><span class="sxs-lookup"><span data-stu-id="0e099-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="0e099-166">Özet</span><span class="sxs-lookup"><span data-stu-id="0e099-166">Summary</span></span>
<span data-ttu-id="0e099-167">Merhaba kurulumu tamamladıktan sonra toouse hello esnek veritabanı istemci kitaplığı başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e099-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="0e099-168">Aynı zamanda [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) ve [çok parça sorgu](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e099-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e099-169">Next steps</span></span>
<span data-ttu-id="0e099-170">Gelen Hello PowerShell komut dosyalarını almak [Azure SQL DB esnek veritabanı araçlarını sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="0e099-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="0e099-171">Merhaba araçlardır de Github'da: [Azure/esnek-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="0e099-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="0e099-172">Merhaba bölünmüş Birleştirme aracı toomove veri tooor çok kiracılı bir model tooa tek bir kiracı modelden kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e099-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="0e099-173">Bkz: [bölünmüş Birleştirme aracı](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e099-174">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0e099-174">Additional resources</span></span>
<span data-ttu-id="0e099-175">Çok kiracılı hizmet olarak yazılım (SaaS) veritabanı uygulamalarının ortak veri mimarisi düzenlerine ilişkin bilgi için bkz. [Azure SQL Database ile Çok Kiracılı SaaS Uygulamaları için Tasarım Düzenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0e099-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="0e099-176">Sorular ve özellik istekleri</span><span class="sxs-lookup"><span data-stu-id="0e099-176">Questions and Feature Requests</span></span>
<span data-ttu-id="0e099-177">Sorular için lütfen hello üzerinde toous ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekleri için lütfen toohello eklemesini [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0e099-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

