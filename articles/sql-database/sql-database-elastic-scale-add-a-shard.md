---
title: "Esnek veritabanı araçlarını kullanarak parça a aaaAdding | Microsoft Docs"
description: "Nasıl toouse esnek ölçeklendirme API'leri tooadd yeni parça tooa parça ayarlayın."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="cae0f-103">Esnek veritabanı araçlarını kullanarak bir parça ekleme</span><span class="sxs-lookup"><span data-stu-id="cae0f-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="cae0f-104">Yeni aralık veya anahtarı için bir parça tooadd</span><span class="sxs-lookup"><span data-stu-id="cae0f-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="cae0f-105">Uygulamaları parça eşleme zaten var için toosimply yeni anahtarlar veya anahtar aralıkları, beklenen yeni parça toohandle veriler genellikle eklemeniz.</span><span class="sxs-lookup"><span data-stu-id="cae0f-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="cae0f-106">Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı tooprovision yeni bir parça gerekebilir veya veri parçalı aylık yeni her ay hello başlamadan önce sağlanan yeni bir parça gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="cae0f-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="cae0f-107">Anahtar değerlerinin Hello yeni aralık zaten varolan bir eşleme parçası değilse çok basit tooadd hello yeni parça ve ilişkilendirme hello yeni anahtarı veya aralık toothat parça olur.</span><span class="sxs-lookup"><span data-stu-id="cae0f-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="cae0f-108">Örnek: bir parça ve kendi aralığı tooan varolan parça eşleme ekleme</span><span class="sxs-lookup"><span data-stu-id="cae0f-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="cae0f-109">Bu örnek hello kullanan [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) yöntemleri ve hello örneği oluşturur [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cae0f-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="cae0f-110">Aşağıda, adlı bir veritabanı hello örnekteki **sample_shard_2** ve içindeki tüm gerekli şema nesneleri toohold aralığı [300, 400). oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="cae0f-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="cae0f-111">Alternatif olarak, Powershell toocreate yeni parça eşleme Yöneticisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cae0f-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="cae0f-112">Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="cae0f-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="cae0f-113">var olan bir aralığı boş bir kısmı için bir parça tooadd</span><span class="sxs-lookup"><span data-stu-id="cae0f-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="cae0f-114">Bazı durumlarda, bir aralık tooa parça eşlenmiş ve kısmen verilerle doldurulur olabilirsiniz, ancak şimdi yaklaşan veri toobe yönlendirilmiş tooa farklı parça istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="cae0f-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="cae0f-115">Örneğin, parça günlük aralığı ve 50 gün tooa parça Tahsis etmiş ancak farklı bir parça, gelecekteki veri tooland istediğiniz 24 günü.</span><span class="sxs-lookup"><span data-stu-id="cae0f-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="cae0f-116">Merhaba esnek veritabanı [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu işlemi gerçekleştirebilir, ancak veri taşıma yani (örneğin, günlük [25, 50 hello aralığı için veri), gerekli değilse gün 25 dahil too50 özel, henüz yok), gerçekleştirebilirsiniz tamamen kullanarak bu hello parça eşleme Yönetimi API'lerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="cae0f-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="cae0f-117">Örnek: bir aralık bölme ve hello atama bölümü tooa yeni eklenen parça boş</span><span class="sxs-lookup"><span data-stu-id="cae0f-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="cae0f-118">"Sample_shard_2" ve içindeki tüm gerekli şema nesneleri adlı bir veritabanı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cae0f-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="cae0f-119">**Önemli**: aralığının hello belirli varsa güncelleştirilmiş hello eşleme boş, yalnızca bu tekniği kullanın.</span><span class="sxs-lookup"><span data-stu-id="cae0f-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="cae0f-120">Yukarıdaki Hello yöntemleri taşınan hello aralığı için veri denetleme, en iyi şekilde kodunuzda tooinclude denetler.</span><span class="sxs-lookup"><span data-stu-id="cae0f-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="cae0f-121">Satırlar taşınan hello aralığında varsa, hello gerçek veri dağıtım hello güncelleştirilmiş parça eşleme eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="cae0f-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="cae0f-122">Kullanım hello [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello işlemi bunun yerine bu gibi durumlarda.</span><span class="sxs-lookup"><span data-stu-id="cae0f-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

