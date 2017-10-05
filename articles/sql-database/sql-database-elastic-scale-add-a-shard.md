---
title: "Esnek veritabanı araçlarını kullanarak bir parça ekleme | Microsoft Docs"
description: "Esnek ölçeklendirme API'leri yeni parça bir parça eklemek için nasıl kullanılacağını ayarlayın."
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
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="0ba86-103">Esnek veritabanı araçlarını kullanarak bir parça ekleme</span><span class="sxs-lookup"><span data-stu-id="0ba86-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="0ba86-104">Yeni aralık veya anahtarı için bir parça eklemek için</span><span class="sxs-lookup"><span data-stu-id="0ba86-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="0ba86-105">Uygulamalar genellikle yalnızca yeni anahtarlar veya zaten bir parça eşleme için anahtar aralıklarına beklenen verileri işlemek için yeni parça eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ba86-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="0ba86-106">Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı yeni bir parça sağlamak gerekebilir veya veri parçalı aylık yeni her ayın başlangıcını önce sağlanan yeni bir parça gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0ba86-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="0ba86-107">Yeni anahtar değerleri aralığı zaten varolan bir eşleme parçası değilse, yeni parça eklemek ve yeni bir anahtar ya da bu parça aralığa ilişkilendirmek çok daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="0ba86-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="0ba86-108">Örnek: varolan bir parça eşlemesini bir parça ve kendi aralığı ekleme</span><span class="sxs-lookup"><span data-stu-id="0ba86-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="0ba86-109">Bu örnekte [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) yöntemleri ve bir örneğini oluşturur [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.)sınıfı.</span><span class="sxs-lookup"><span data-stu-id="0ba86-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="0ba86-110">Aşağıda, adlı bir veritabanı örneğinde **sample_shard_2** ve içindeki tüm gerekli şema nesneleri [300, 400). aralık tutmak için oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0ba86-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="0ba86-111">Alternatif olarak, yeni parça eşleme Yöneticisi oluşturmak için PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ba86-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="0ba86-112">Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="0ba86-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="0ba86-113">Var olan bir aralığı boş bir kısmı için bir parça eklemek için</span><span class="sxs-lookup"><span data-stu-id="0ba86-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="0ba86-114">Bazı durumlarda, bir parça için bir aralığı zaten eşlenmiş ve kısmen verilerle doldurulur olabilirsiniz, ancak şimdi için farklı bir parça yönlendirilmesi için yaklaşan veri istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0ba86-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="0ba86-115">Örneğin, parça gün aralığı tarafından ve parça için zaten ayrılmış 50 gününüz vardır, ancak gelecekteki verilerin içinde farklı bir parça güden istediğiniz günde 24.</span><span class="sxs-lookup"><span data-stu-id="0ba86-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="0ba86-116">Esnek veritabanı [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu işlemi gerçekleştirebilir, ancak veri taşıma yani (örneğin, [25, 50 gün aralığı için veri), gerekli değilse gün 25 özel, 50 (dahil) henüz yok), bu gerçekleştirebilirsiniz tamamen parça eşleme Yönetimi API'leri kullanarak doğrudan.</span><span class="sxs-lookup"><span data-stu-id="0ba86-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="0ba86-117">Örnek: bir aralık bölme ve yeni eklenen bir parça boş bölümü atama</span><span class="sxs-lookup"><span data-stu-id="0ba86-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="0ba86-118">"Sample_shard_2" ve içindeki tüm gerekli şema nesneleri adlı bir veritabanı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0ba86-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="0ba86-119">**Önemli**: aralığının eminseniz güncelleştirilmiş eşleme boş ise yalnızca bu tekniği kullanın.</span><span class="sxs-lookup"><span data-stu-id="0ba86-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="0ba86-120">Denetimleri kodunuzda dahil etmek en iyisidir yukarıdaki yöntemleri taşınan, aralığı için veri denetlemez.</span><span class="sxs-lookup"><span data-stu-id="0ba86-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="0ba86-121">Satırlar taşınan aralığında varsa, gerçek veri dağıtım güncelleştirilmiş parça eşleme eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="0ba86-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="0ba86-122">Kullanım [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu gibi durumlarda bunun yerine işlemi gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0ba86-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

