---
title: "bir Azure SQL veritabanı çıkışı aaaScale | Microsoft Docs"
description: "Nasıl toouse hello ShardMapManager, esnek veritabanı istemci kitaplığı"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="a925d-103">Merhaba parça eşleme Yöneticisi veritabanlarıyla ölçeğini genişletme</span><span class="sxs-lookup"><span data-stu-id="a925d-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="a925d-104">SQL Azure veritabanı tooeasily ölçeklenebilir bir parça eşleme Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="a925d-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="a925d-105">Merhaba parça eşleme Yöneticisi bir parça kümesindeki tüm parça (veritabanları) hakkında genel eşleme bilgilerini tutan özel bir veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="a925d-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="a925d-106">Merhaba meta veri sağlar hello hello değerini alarak bir uygulama tooconnect toohello doğru veritabanı **parçalama anahtar**.</span><span class="sxs-lookup"><span data-stu-id="a925d-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="a925d-107">Ayrıca, her parça hello kümesindeki hello yerel parça verileri izlemek eşlemeleri içerir (olarak bilinen **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="a925d-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Parça eşleme Yönetimi](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="a925d-109">Bu eşlemeleri nasıl oluşturulur anlama temel tooshard harita yönetimidir.</span><span class="sxs-lookup"><span data-stu-id="a925d-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="a925d-110">Bu yapılır hello kullanarak [ShardMapManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), hello bulunan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) toomanage parça eşler.</span><span class="sxs-lookup"><span data-stu-id="a925d-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="a925d-111">Parça eşlemeleri ve parça eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="a925d-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="a925d-112">Her parça, parça eşleme toocreate hello türü seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a925d-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="a925d-113">Merhaba seçim hello veritabanı mimarisine bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="a925d-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="a925d-114">Veritabanı başına tek bir kiracı</span><span class="sxs-lookup"><span data-stu-id="a925d-114">Single tenant per database</span></span>  
2. <span data-ttu-id="a925d-115">Birden çok Kiracı veritabanı (iki tür) başına:</span><span class="sxs-lookup"><span data-stu-id="a925d-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="a925d-116">Liste eşleme</span><span class="sxs-lookup"><span data-stu-id="a925d-116">List mapping</span></span>
   2. <span data-ttu-id="a925d-117">Aralık eşleme</span><span class="sxs-lookup"><span data-stu-id="a925d-117">Range mapping</span></span>

<span data-ttu-id="a925d-118">Tek Kiracı model için oluşturduğunuz bir **listesi eşleme** parça eşleme.</span><span class="sxs-lookup"><span data-stu-id="a925d-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="a925d-119">Merhaba tek kiracılı bir model Kiracı başına tek bir veritabanı atar.</span><span class="sxs-lookup"><span data-stu-id="a925d-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="a925d-120">Yönetimini basitleştirir gibi SaaS geliştiriciler için etkili bir modeli budur.</span><span class="sxs-lookup"><span data-stu-id="a925d-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Liste eşleme][1]

<span data-ttu-id="a925d-122">Merhaba çok kiracılı bir model çeşitli kiracılar tooa tek veritabanı atar (ve kiracılar grupları birden çok veritabanı arasında dağıtabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="a925d-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="a925d-123">Bu model, her Kiracı toohave küçük veri gereken beklediğiniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="a925d-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="a925d-124">Bu modelde, biz kiracılar tooa veritabanını kullanmanın bir aralığı atamak **aralığı eşleme**.</span><span class="sxs-lookup"><span data-stu-id="a925d-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Aralık eşleme][2]

<span data-ttu-id="a925d-126">Veya, bir çok Kiracı veritabanı modelini kullanarak uygulayabileceğiniz bir *listesi eşleme* tooassign birden çok kiracılar tooa tek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a925d-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="a925d-127">Örneğin, Kiracı kimliği 1 ve 5 kullanılan toostore bilgilerini DB1 olduğu ve DB2 7 Kiracı ve Kiracı 10 için verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="a925d-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Birden fazla kiracılar tek DB][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="a925d-129">Parçalama anahtarları için desteklenen .net türleri</span><span class="sxs-lookup"><span data-stu-id="a925d-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="a925d-130">.NET aşağıdaki esnek ölçek destek hello Framework parçalama anahtarları olarak türleri:</span><span class="sxs-lookup"><span data-stu-id="a925d-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="a925d-131">tamsayı</span><span class="sxs-lookup"><span data-stu-id="a925d-131">integer</span></span>
* <span data-ttu-id="a925d-132">uzun</span><span class="sxs-lookup"><span data-stu-id="a925d-132">long</span></span>
* <span data-ttu-id="a925d-133">GUID</span><span class="sxs-lookup"><span data-stu-id="a925d-133">guid</span></span>
* <span data-ttu-id="a925d-134">Byte]</span><span class="sxs-lookup"><span data-stu-id="a925d-134">byte[]</span></span>  
* <span data-ttu-id="a925d-135">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="a925d-135">datetime</span></span>
* <span data-ttu-id="a925d-136">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a925d-136">timespan</span></span>
* <span data-ttu-id="a925d-137">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a925d-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="a925d-138">Liste ve aralığı parça eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="a925d-138">List and range shard maps</span></span>
<span data-ttu-id="a925d-139">Parça eşlemeleri kullanarak olacak oluşturulan **tek tek parçalama listesi anahtar değerlerini**, veya kullanılarak oluşturulabilir **parçalama aralıklarına anahtar değerlerini**.</span><span class="sxs-lookup"><span data-stu-id="a925d-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="a925d-140">Liste parça eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="a925d-140">List shard maps</span></span>
<span data-ttu-id="a925d-141">**Parça** içeren **shardlets** ve shardlets tooshards hello eşlenmesini parça eşleme tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="a925d-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="a925d-142">A **listesi parça eşleme** hello shardlets tanımlayan hello tek tek anahtar değerleri ve parça hizmet hello veritabanları arasındaki ilişkidir.</span><span class="sxs-lookup"><span data-stu-id="a925d-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="a925d-143">**Liste eşlemeleri** açık ve farklı anahtar değerleri eşlenen toohello olabilir aynı veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a925d-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="a925d-144">Örneğin, anahtar 1 tooDatabase A eşler ve anahtar değerlerinin 3 ile 6 veritabanı B. başvurusu</span><span class="sxs-lookup"><span data-stu-id="a925d-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="a925d-145">Anahtar</span><span class="sxs-lookup"><span data-stu-id="a925d-145">Key</span></span> | <span data-ttu-id="a925d-146">Parça konumu</span><span class="sxs-lookup"><span data-stu-id="a925d-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a925d-147">1</span><span class="sxs-lookup"><span data-stu-id="a925d-147">1</span></span> |<span data-ttu-id="a925d-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="a925d-148">Database_A</span></span> |
| <span data-ttu-id="a925d-149">3</span><span class="sxs-lookup"><span data-stu-id="a925d-149">3</span></span> |<span data-ttu-id="a925d-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="a925d-150">Database_B</span></span> |
| <span data-ttu-id="a925d-151">4</span><span class="sxs-lookup"><span data-stu-id="a925d-151">4</span></span> |<span data-ttu-id="a925d-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="a925d-152">Database_C</span></span> |
| <span data-ttu-id="a925d-153">6</span><span class="sxs-lookup"><span data-stu-id="a925d-153">6</span></span> |<span data-ttu-id="a925d-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="a925d-154">Database_B</span></span> |
| <span data-ttu-id="a925d-155">...</span><span class="sxs-lookup"><span data-stu-id="a925d-155">...</span></span> |<span data-ttu-id="a925d-156">...</span><span class="sxs-lookup"><span data-stu-id="a925d-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="a925d-157">Aralık parça eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="a925d-157">Range shard maps</span></span>
<span data-ttu-id="a925d-158">İçinde bir **aralığı parça eşleme**, hello anahtar aralığı çifti tarafından açıklanan **[düşük değeri, yüksek değerli)** burada hello *düşük değer* hello minimum anahtarı hello aralığı ve hello *Yüksek değerli* hello ilk değer hello aralığından daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="a925d-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="a925d-159">Örneğin, **[0, 100)** 0 veya daha büyük ve 100'den küçük tüm tamsayılar içerir.</span><span class="sxs-lookup"><span data-stu-id="a925d-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="a925d-160">Birden çok aralıkları can noktası aynı veritabanı ve ayrık aralıkları toohello desteklenir unutmayın (örneğin, [100,200) ve [400,600) iki nokta tooDatabase C hello örnekte.)</span><span class="sxs-lookup"><span data-stu-id="a925d-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="a925d-161">Anahtar</span><span class="sxs-lookup"><span data-stu-id="a925d-161">Key</span></span> | <span data-ttu-id="a925d-162">Parça konumu</span><span class="sxs-lookup"><span data-stu-id="a925d-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a925d-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="a925d-163">[1,50)</span></span> |<span data-ttu-id="a925d-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="a925d-164">Database_A</span></span> |
| <span data-ttu-id="a925d-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="a925d-165">[50,100)</span></span> |<span data-ttu-id="a925d-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="a925d-166">Database_B</span></span> |
| <span data-ttu-id="a925d-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="a925d-167">[100,200)</span></span> |<span data-ttu-id="a925d-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="a925d-168">Database_C</span></span> |
| <span data-ttu-id="a925d-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="a925d-169">[400,600)</span></span> |<span data-ttu-id="a925d-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="a925d-170">Database_C</span></span> |
| <span data-ttu-id="a925d-171">...</span><span class="sxs-lookup"><span data-stu-id="a925d-171">...</span></span> |<span data-ttu-id="a925d-172">...</span><span class="sxs-lookup"><span data-stu-id="a925d-172">...</span></span> |

<span data-ttu-id="a925d-173">Yukarıda gösterilen hello tablolardan her biri kavramsal bir örneği olan bir **ShardMap** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a925d-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="a925d-174">Her satırda tek bir Basitleştirilmiş örneğidir **PointMapping** (için hello listesi parça eşleme) veya **RangeMapping** (için hello aralığı parça eşleme) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a925d-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="a925d-175">Parça eşleme Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="a925d-175">Shard map manager</span></span>
<span data-ttu-id="a925d-176">Merhaba istemci Kitaplığı'nda hello parça eşleme Yöneticisi parça eşlemeleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a925d-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="a925d-177">Merhaba veri tarafından yönetilen bir **ShardMapManager** örneği üç yerde tutulur:</span><span class="sxs-lookup"><span data-stu-id="a925d-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="a925d-178">**Genel parça eşleme (GSM)**: tüm parça eşlemeleri ve eşlemeler için hello depo olarak bir veritabanı tooserve belirtin.</span><span class="sxs-lookup"><span data-stu-id="a925d-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="a925d-179">Özel tabloları ve saklı yordamlar toomanage hello bilgileri otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a925d-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="a925d-180">Bu genellikle küçük bir veritabanı ve hafifçe erişilen ve diğer Merhaba uygulaması gereksinimleriniz için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a925d-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="a925d-181">Merhaba adlı özel bir şemada tablolardır **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="a925d-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="a925d-182">**Yerel parça eşleme (LSM)**: bir parça olduğu toobe değiştiren toocontain birkaç küçük tablolar ve parça eşleme bilgilerini belirli toothat parça yönetmek ve içeren özel saklı yordamlar belirttiğiniz her veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a925d-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="a925d-183">Bu bilgiler hello GSM hello bilgilerle yedekli ve GSM hello üzerinde hiçbir yük koymadan hello uygulama önbelleğe toovalidate parça eşleme bilgilerini sağlar; önbelleğe alınan bir eşleme hala geçerli ise Merhaba uygulaması hello LSM toodetermine kullanır.</span><span class="sxs-lookup"><span data-stu-id="a925d-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="a925d-184">Merhaba tabloları her parça üzerinde LSM olan ayrıca hello şemada karşılık gelen toohello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="a925d-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="a925d-185">**Uygulama önbelleği**: her uygulama örneği erişen bir **ShardMapManager** nesne eşlemelerini, yerel bir bellek içi önbellek tutar.</span><span class="sxs-lookup"><span data-stu-id="a925d-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="a925d-186">Son alınan yönlendirme bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="a925d-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="a925d-187">Bir ShardMapManager oluşturma</span><span class="sxs-lookup"><span data-stu-id="a925d-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="a925d-188">A **ShardMapManager** nesnesi kullanılarak yapılandırılmıştır bir [Fabrika](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) düzeni.</span><span class="sxs-lookup"><span data-stu-id="a925d-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="a925d-189">Merhaba  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  yöntemi alır (Merhaba sunucu adını ve veritabanı adını hello GSM bulunduran dahil) kimlik bilgilerini hello biçiminde bir  **ConnectionString** ve bir örneğini döndüren bir **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="a925d-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="a925d-190">**Lütfen dikkat edin:** hello **ShardMapManager** hello başlatma kodundaki bir uygulama için uygulama etki alanı başına yalnızca bir kez örneğinin oluşturulması.</span><span class="sxs-lookup"><span data-stu-id="a925d-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="a925d-191">Oluşturma ek ShardMapManager durumlarda Merhaba, aynı appdomain sonuçlanacak artan bellek ve CPU kullanımını Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a925d-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="a925d-192">A **ShardMapManager** parça eşlemelerinin herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a925d-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="a925d-193">Bir tek parça eşleme birçok uygulama için yeterli olabilir, ancak veritabanlarının farklı kümeleri farklı şema veya benzersiz amacıyla kullanıldığında zamanlar vardır; Bu gibi durumlarda birden fazla parça eşlemeleri tercih edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a925d-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="a925d-194">Bu kodda tooopen var olan bir uygulama çalışırsa **ShardMapManager** hello ile [TryGetSqlShardMapManager yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a925d-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="a925d-195">Varsa bir genel temsil eden nesneler **ShardMapManager** (GSM) sağlamadığı henüz hello veritabanı içinde var, hello istemci kitaplığı oluşturur bunları orada hello kullanarak [CreateSqlShardMapManager yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a925d-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="a925d-196">Alternatif olarak, Powershell toocreate yeni parça eşleme Yöneticisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a925d-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="a925d-197">Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a925d-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="a925d-198">RangeShardMap veya ListShardMap Al</span><span class="sxs-lookup"><span data-stu-id="a925d-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="a925d-199">Bir parça eşleme Yöneticisi oluşturduktan sonra hello alabilirsiniz [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) veya [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello kullanarak [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), veya hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a925d-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="a925d-200">Parça eşleme yönetim kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="a925d-200">Shard map administration credentials</span></span>
<span data-ttu-id="a925d-201">Yönetmek ve parça eşlemeleri işlemek hello parça eşlemeleri tooroute bağlantılarını kullanan olanlardan farklı uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="a925d-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="a925d-202">tooadminister parça eşlemeleri (ekleme veya değiştirme parça parça eşlemeleri, parça eşlemeleri, vb.) hello oluşturmalıdır **ShardMapManager** kullanarak **sahip kimlik bilgileri okuma/yazma hem hello GSM veritabanı ve her ayrıcalıklarını Parça hizmet veren veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="a925d-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="a925d-203">Parça eşleme bilgisi girilen ya da üzerinde yeni parça LSM tablo oluşturma için olduğu gibi değiştirilmiş hello kimlik bilgileri hem hello hello tablolarda karşı yazmalar için GSM ve LSM izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a925d-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="a925d-204">Bkz: [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="a925d-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="a925d-205">Yalnızca etkilenen meta veriler</span><span class="sxs-lookup"><span data-stu-id="a925d-205">Only metadata affected</span></span>
<span data-ttu-id="a925d-206">Doldurma veya hello değiştirmek için kullanılan yöntemleri **ShardMapManager** veri hello parça kendilerini depolanan hello kullanıcı verilerini alter değil.</span><span class="sxs-lookup"><span data-stu-id="a925d-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="a925d-207">Örneğin, yöntemler gibi **CreateShard**, **DeleteShard**, **UpdateMapping**, vb. hello parça eşlemesi meta verileri yalnızca etkiler.</span><span class="sxs-lookup"><span data-stu-id="a925d-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="a925d-208">Bunlar kaldırmayın, ekleyebilir veya hello parça bulunan kullanıcı verileri alter.</span><span class="sxs-lookup"><span data-stu-id="a925d-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="a925d-209">Bunun yerine, bu yöntemleri kullanılan tasarlanmış toobe olan ayrı işlemleri ile birlikte toocreate gerçekleştirmek veya gerçek veritabanlarını kaldırmanız ya da bu taşıma parçalı bir ortamda bir parça tooanother toorebalance satırlar.</span><span class="sxs-lookup"><span data-stu-id="a925d-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="a925d-210">(Merhaba **bölünmüş birleştirme** esnek veritabanı araçları ile içerdiği aracı yapar parça arasında gerçek veri taşıma yönetme yanı sıra bu API'leri kullanın.) Bkz: [ölçeklendirme hello esnek veritabanı bölünmüş-birleştirme aracını kullanarak](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="a925d-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="a925d-211">Bir parça eşleme örneği doldurma</span><span class="sxs-lookup"><span data-stu-id="a925d-211">Populating a shard map example</span></span>
<span data-ttu-id="a925d-212">Bir örnek dizisi işlemleri toopopulate belirli parça eşleme, aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a925d-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="a925d-213">Merhaba kod aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="a925d-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="a925d-214">Yeni bir parça eşleme parça eşleme manager içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a925d-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="a925d-215">iki farklı parça Hello meta verilerini toohello parça eşleme eklenir.</span><span class="sxs-lookup"><span data-stu-id="a925d-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="a925d-216">Anahtar aralığı eşlemeleri çeşitli eklenir ve hello genel içeriği hello parça eşleme görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a925d-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="a925d-217">böylece bir hata oluşursa hello yöntemi yeniden çalıştırılabilir hello kodu yazılır.</span><span class="sxs-lookup"><span data-stu-id="a925d-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="a925d-218">Her istek bir parça olup olmadığını sınar veya eşleme zaten var, toocreate denemeden önce onu.</span><span class="sxs-lookup"><span data-stu-id="a925d-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="a925d-219">Merhaba kod veritabanları adlı varsayar **sample_shard_0**, **sample_shard_1** ve **sample_shard_2** dizesitarafındanbaşvurulanhelloServer'dakizatenoluşturulmuş**shardServer**.</span><span class="sxs-lookup"><span data-stu-id="a925d-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="a925d-220">Tooachieve hello PowerShell kullanabileceğiniz alternatif komutlar aynı sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a925d-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="a925d-221">Merhaba örnek PowerShell örnekleri bazıları kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a925d-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="a925d-222">Parça eşlemeleri doldurulduğunu sonra veri erişimi uygulamaları oluşturulabilir veya toowork hello Haritalar ile uyarlanan.</span><span class="sxs-lookup"><span data-stu-id="a925d-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="a925d-223">Doldurma veya hello eşlemeleri düzenleme gerçekleşmediği kadar yeniden **harita düzeni** toochange gerekir.</span><span class="sxs-lookup"><span data-stu-id="a925d-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="a925d-224">Verilere bağımlı yönlendirme</span><span class="sxs-lookup"><span data-stu-id="a925d-224">Data dependent routing</span></span>
<span data-ttu-id="a925d-225">Merhaba parça eşleme Yöneticisi en veritabanı bağlantılarını tooperform hello uygulamaya özgü verileri işlemleri gerektiren uygulamalarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a925d-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="a925d-226">Bu bağlantılar hello doğru veritabanı ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a925d-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="a925d-227">Bu olarak bilinir **veri bağımlı yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="a925d-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="a925d-228">Bu uygulamalar için hello Fabrika hello GSM veritabanında salt okunur erişime sahip kimlik bilgilerini kullanarak bir parça eşleme Yöneticisi nesneden örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a925d-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="a925d-229">Daha sonraki bağlantılar için istekleri ayrı ayrı toohello uygun parça veritabanına bağlanmak için gereken kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a925d-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="a925d-230">Unutmayın bu uygulamaları (kullanarak **ShardMapManager** salt okunur kimlik bilgileriyle açılan) değişiklik toohello eşlemeleri veya eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="a925d-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="a925d-231">Bu ihtiyaçları için özel yönetim uygulamalarını ya da daha önce bahsedildiği gibi daha yüksek ayrıcalıklı kimlik bilgilerini sağlamanız PowerShell komut dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a925d-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="a925d-232">Bkz: [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="a925d-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="a925d-233">Daha fazla ayrıntı için bkz: [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="a925d-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="a925d-234">Parça eşlemeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="a925d-234">Modifying a shard map</span></span>
<span data-ttu-id="a925d-235">Parça eşleme farklı şekilde değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a925d-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="a925d-236">Tüm yöntemleri aşağıdaki hello hello parça ve bu nesnelerin eşlemelerini açıklayan hello meta verilerini değiştirmek ancak fiziksel olarak veri hello parça içinde değiştirmeyin ve bunlar oluşturmak veya hello gerçek veritabanlarını silin.</span><span class="sxs-lookup"><span data-stu-id="a925d-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="a925d-237">Aşağıda açıklanan hello parça eşleme hello işlemleri bazıları, fiziksel olarak veri taşıma veya ekleyin ve parça hizmet veren veritabanlarını kaldırmanız yönetim eylemleri ile eşgüdümlü toobe gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a925d-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="a925d-238">Bu yöntemler hello yapı taşları değiştirmek için kullanılabilir olarak birlikte çalışan hello parçalı veritabanı ortamınızdaki verilerin genel dağıtım.</span><span class="sxs-lookup"><span data-stu-id="a925d-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="a925d-239">tooadd veya kaldırma parça: kullanmak  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  ve  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Merhaba, [Shardmap sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="a925d-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="a925d-240">Merhaba sunucu ve veritabanı hello hedef parça temsil eden bu işlemleri tooexecute için varolmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a925d-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="a925d-241">Bu yöntemlerin herhangi bir etki hello veritabanlarında kendileri yalnızca meta veri hello parça eşlemesindeki üzerinde sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="a925d-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="a925d-242">toocreate veya kaldırma noktaları veya aralıklarını eşlenen toohello parça: kullanmak  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  Merhaba, [RangeShardMapping sınıfı](https://msdn.microsoft.com/library/azure/dn807318.aspx), ve  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Merhaba, [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="a925d-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="a925d-243">Birçok farklı noktaları veya aralıklar eşlenen toohello olabilir aynı parça.</span><span class="sxs-lookup"><span data-stu-id="a925d-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="a925d-244">Bu yöntemler, yalnızca meta veri etkiler - zaten parça içinde bulunabilecek herhangi bir veri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="a925d-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="a925d-245">Veri sırası toobe ile tutarlı hello veritabanından kaldırılmış toobe gerekip gerekmediğini **DeleteMapping** işlemleri ayrı olarak, ancak bu yöntemleri kullanarak ile birlikte bu işlemler tooperform gerekir.</span><span class="sxs-lookup"><span data-stu-id="a925d-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="a925d-246">iki veya tek bir birleştirme bitişik aralıkları toosplit varolan aralıkları: kullanmak  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  ve  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="a925d-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="a925d-247">Bölme ve birleştirme işlemlerinin unutmayın **hello parça toowhich anahtar değerleri eşlendi değiştirmeyin**.</span><span class="sxs-lookup"><span data-stu-id="a925d-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="a925d-248">Bölme iki bölüme var olan bir aralığı keser, ancak hem eşleşen toohello olarak bırakır aynı parça.</span><span class="sxs-lookup"><span data-stu-id="a925d-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="a925d-249">Bir birleştirme zaten eşlenmiş toohello olan iki bitişik aralıkları çalışır tek bir aralığa birleştirmesi aynı parça.</span><span class="sxs-lookup"><span data-stu-id="a925d-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="a925d-250">Merhaba noktaları veya aralıklar kendilerini parça arasında hareketini gereken kullanarak Eşgüdümlü toobe **UpdateMapping** gerçek veri taşıma birlikte.</span><span class="sxs-lookup"><span data-stu-id="a925d-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="a925d-251">Merhaba kullanabilirsiniz **bölünmüş/Merge** hizmetinin esnek veritabanı parçası olan araçlar toocoordinate parça eşleme veri taşıma değişikliklerle taşıması gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="a925d-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="a925d-252">toore eşleme (veya taşıma) tek tek nokta veya aralıklar toodifferent parça: kullanmak  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="a925d-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="a925d-253">Verileri bir parça tooanother sipariş toobe ile tutarlı olarak taşınmıştır toobe gerekebileceği **UpdateMapping** işlemleri tooperform ayrı olarak, ancak bu yöntemleri kullanarak ile birlikte bu taşıması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a925d-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="a925d-254">tootake eşlemeleri çevrimiçi ve çevrimdışı: kullanmak  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  ve  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello çevrimiçi durumunu bir eşleme.</span><span class="sxs-lookup"><span data-stu-id="a925d-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="a925d-255">Bir eşleme "Çevrimdışı" bir durumda olduğunda parça eşlemeleri üzerindeki belirli işlemlerin yalnızca verilir dahil olmak üzere **UpdateMapping** ve **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="a925d-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="a925d-256">Bir eşleme çevrimdışı olduğunda, o eşlemeye dahil bir anahtarı temel alan bir veri bağımlı istek bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="a925d-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="a925d-257">Ayrıca, bir aralık önce çevrimdışı duruma getirildiğinde, tüm bağlantılar etkilenen toohello parça otomatik olarak sonlandırıldı sonuçlarında sipariş tooprevent tutarsız veya tamamlanmamış değiştirilmesini aralıkları karşı yönlendirilmiş sorgular için.</span><span class="sxs-lookup"><span data-stu-id="a925d-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="a925d-258">Eşlemeleri .net içinde değişmez nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="a925d-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="a925d-259">Tüm eşlemelerini değiştirmek hello yöntemleri yukarıdaki da kodunuzdaki tüm başvuruları toothem geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a925d-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="a925d-260">toomake bir eşlemeyi değiştirmek hello yöntemleri tümünün eşleme 's durumunu değiştirme işlemleri daha kolay tooperform dizilerini dönüş yeni bir BT işlemleri yapılabilmesi için başvuru, eşleme.</span><span class="sxs-lookup"><span data-stu-id="a925d-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="a925d-261">Örneğin, mevcut bir başlangıç anahtarı 25 içeren shardmap sm içinde eşleme toodelete aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a925d-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="a925d-262">Bir parça ekleme</span><span class="sxs-lookup"><span data-stu-id="a925d-262">Adding a shard</span></span>
<span data-ttu-id="a925d-263">Uygulamaları parça eşleme zaten var için toosimply yeni anahtarlar veya anahtar aralıkları, beklenen yeni parça toohandle veriler genellikle eklemeniz.</span><span class="sxs-lookup"><span data-stu-id="a925d-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="a925d-264">Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı tooprovision yeni bir parça gerekebilir veya veri parçalı aylık yeni her ay hello başlamadan önce sağlanan yeni bir parça gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a925d-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="a925d-265">Anahtar değerlerinin Hello yeni aralık zaten yoksa varolan eşlemesini ve hiçbir veri taşıma parçası çok basit tooadd hello yeni parça olduğu gereklidir ve hello yeni bir anahtar ya da aralığı toothat parça ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a925d-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="a925d-266">Yeni parça ekleme hakkında daha fazla bilgi için bkz: [yeni bir parça eklemek](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="a925d-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="a925d-267">Veri taşıma gerektiren senaryolar için ancak hello bölünmüş birleştirme gerekli tooorchestrate hello veri taşıma hello gerekli parça eşleme güncelleştirmeleri ile birlikte parça arasında aracıdır.</span><span class="sxs-lookup"><span data-stu-id="a925d-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="a925d-268">Bölünmüş birleştirme yool kullanımıyla ilgili ayrıntılar hello için bkz: [bölünmüş birleştirme genel bakış](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="a925d-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
