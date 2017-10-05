---
title: "Esnek veritabanı araçlarını sözlüğü | Microsoft Docs"
description: "Esnek veritabanı araçları için kullanılan terimler açıklaması"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="cd9fb-103">Esnek veritabanı araçlarını sözlüğü</span><span class="sxs-lookup"><span data-stu-id="cd9fb-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="cd9fb-104">Aşağıdaki terimler için tanımlanan [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md), Azure SQL veritabanı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="cd9fb-105">Araçlar yönetmek için kullanılan [parça eşlemeleri](sql-database-elastic-scale-shard-map-management.md)ve dahil [istemci Kitaplığı](sql-database-elastic-database-client-library.md), [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md), [esnek havuzlar](sql-database-elastic-pool.md)ve [sorguları](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd9fb-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="cd9fb-106">Aşağıdaki terimler kullanılır [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [parça eşleme sorunları düzeltmek için RecoveryManager sınıfını kullanarak](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd9fb-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Esnek ölçeklendirme koşulları][1]

<span data-ttu-id="cd9fb-108">**Veritabanı**: bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="cd9fb-109">**Veri bağımlı yönlendirme**: belirli parçalama anahtara verilen bir parça bağlanmak bir uygulama sağlayan işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="cd9fb-110">Bkz: [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="cd9fb-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="cd9fb-111">Karşılaştırılacak  **[çok parça sorgu](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="cd9fb-112">**Genel parça eşleme**: parçalama anahtarları ve bunların ilgili parça içinde arasında eşleme bir **parça kümesi**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="cd9fb-113">Genel parça eşleme depolanan **parça eşleme Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="cd9fb-114">Karşılaştırılacak **yerel parça eşleme**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="cd9fb-115">**Liste parça eşleme**: bir parça eşleme hangi parçalama anahtarları ayrı ayrı eşlendi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="cd9fb-116">Karşılaştırılacak **aralığı parça eşleme**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="cd9fb-117">**Yerel parça eşleme**: parça üzerinde depolanan, yerel parça eşleme parça üzerinde bulunan shardlets eşlemeler içerir.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="cd9fb-118">**Çok parça sorgu**: birden çok parça; bir sorgu verme özelliği sonuç kümeleri, UNION ALL semantiği (olarak da bilinen "yayma sorgu") kullanılarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="cd9fb-119">Karşılaştırılacak **veri bağımlı yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="cd9fb-120">**Çok kiracılı** ve **tek Kiracı**: Bu tek Kiracı veritabanı ve çok Kiracı veritabanı gösterir:</span><span class="sxs-lookup"><span data-stu-id="cd9fb-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="cd9fb-122">Bir gösterimini işte **parçalı** tek ve çoklu kiracı veritabanları.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="cd9fb-124">**Aralık parça eşleme**: bir parça eşleme parça Dağıtım stratejisi birden çok bitişik değerleri aralığı üzerinde dayanır.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="cd9fb-125">**Başvuru tabloları**: parçalı değildir ancak parça arasında çoğaltılan tabloları.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="cd9fb-126">Örneğin, posta kodları başvuru tablosunda depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="cd9fb-127">**Parça**: parçalı bir veri kümesinden veri depolayan bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="cd9fb-128">**Parça esneklik**: her ikisi de gerçekleştirme yeteneğini **yatay ölçekleme** ve **dikey ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="cd9fb-129">**Parçalı tabloları**: tabloları, parçalı, başka bir deyişle, verileri parçalama anahtar değerlerine göre parça dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="cd9fb-130">**Parçalama anahtar**: veri parça arasında nasıl dağıtıldığını belirler bir sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="cd9fb-131">Değer türü şunlardan biri olabilir: **int**, **bigint**, **varbinary**, veya **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="cd9fb-132">**Parça kümesi**: parça eşleme Yöneticisi'nde aynı parça eşlemeye öznitelikli parça koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="cd9fb-133">**Shardlet**: tüm tek bir parça bir parçalama anahtar değeriyle ilişkilendirilmiş veriler.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="cd9fb-134">Bir shardlet en küçük olası veri taşıma parçalı tabloları dağıtırken birimidir.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="cd9fb-135">**Parça eşleme**: parçalama anahtarları ve bunların ilgili parça arasındaki eşlemeleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="cd9fb-136">**Parça eşleme Yöneticisi**: parça harita(lar), parça konumları ve bir veya daha fazla parça kümeleri için eşlemelerini içeren bir Yönetim nesnesi ve veri deposu.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Eşlemeleri][2]

## <a name="verbs"></a><span data-ttu-id="cd9fb-138">Fiiller</span><span class="sxs-lookup"><span data-stu-id="cd9fb-138">Verbs</span></span>
<span data-ttu-id="cd9fb-139">**Yatay ölçekleme**: (veya) ölçeklendirme eylemi ekleyerek veya parça parça eşleme için aşağıda gösterildiği gibi kaldırarak parça koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Yatay ve dikey ölçekleme][3]

<span data-ttu-id="cd9fb-141">**Birleştirme**: taşıma shardlets iki parça için bir parça ve parça eşleme uygun şekilde güncelleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="cd9fb-142">**Shardlet taşıma**: tek bir shardlet için farklı bir parça taşıma işlemi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="cd9fb-143">**Parça**: bir parçalama anahtarına göre birden fazla veritabanı üzerinden yapısal verileri yatay olarak aynı bölümleme eylemi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="cd9fb-144">**Bölünmüş**: birkaç shardlets bir parça için başka bir (genellikle yeni) parça taşıma işlemi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="cd9fb-145">Bir parçalama anahtar bölünmüş noktası olarak kullanıcı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="cd9fb-146">**Dikey ölçeklendirme**: Yukarı (veya aşağı) ölçeklendirme eylemi tek tek bir parça performans düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="cd9fb-147">Örneğin, bir parça (ve daha fazla bilgi işlem kaynakları sonuçlanır) Premium'a standart değiştirme.</span><span class="sxs-lookup"><span data-stu-id="cd9fb-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

