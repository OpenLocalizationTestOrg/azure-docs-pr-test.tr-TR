---
title: "aaaElastic veritabanı araçları sözlüğü | Microsoft Docs"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="ba3d5-103">Esnek veritabanı araçlarını sözlüğü</span><span class="sxs-lookup"><span data-stu-id="ba3d5-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="ba3d5-104">Merhaba aşağıdaki terimler hello için tanımlanan [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md), Azure SQL veritabanı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="ba3d5-105">Merhaba kullanılan toomanage araçlardır [parça eşlemeleri](sql-database-elastic-scale-shard-map-management.md)ve hello dahil [istemci Kitaplığı](sql-database-elastic-database-client-library.md), hello [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md), [esnek havuzlar](sql-database-elastic-pool.md), ve [sorguları](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba3d5-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="ba3d5-106">Aşağıdaki terimler kullanılır [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [hello RecoveryManager sınıfı toofix parça eşlemesi sorunlarının kullanarak](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ba3d5-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Esnek ölçeklendirme koşulları][1]

<span data-ttu-id="ba3d5-108">**Veritabanı**: bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="ba3d5-109">**Veri bağımlı yönlendirme**: Merhaba belirli parçalama anahtara verilen bir uygulama tooconnect tooa parça sağlayan işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="ba3d5-110">Bkz: [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="ba3d5-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="ba3d5-111">Çok karşılaştırma**[çok parça sorgu](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="ba3d5-112">**Genel parça eşleme**: hello harita parçalama anahtarları ve bunların ilgili parça içinde arasında bir **parça kümesi**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="ba3d5-113">Merhaba genel parça eşleme hello depolanan **parça eşleme Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="ba3d5-114">Çok karşılaştırma**yerel parça eşleme**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="ba3d5-115">**Liste parça eşleme**: bir parça eşleme hangi parçalama anahtarları ayrı ayrı eşlendi.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="ba3d5-116">Çok karşılaştırma**aralığı parça eşleme**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="ba3d5-117">**Yerel parça eşleme**: parça üzerinde depolanan, hello yerel parça eşleme hello parça üzerinde bulunan hello shardlets eşlemeler içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="ba3d5-118">**Çok parça sorgu**: özelliği tooissue bir sorgu birden fazla parça hello; sonuç kümeleri, UNION ALL semantiği (olarak da bilinen "yayma sorgu") kullanılarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="ba3d5-119">Çok karşılaştırma**veri bağımlı yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="ba3d5-120">**Çok kiracılı** ve **tek Kiracı**: Bu tek Kiracı veritabanı ve çok Kiracı veritabanı gösterir:</span><span class="sxs-lookup"><span data-stu-id="ba3d5-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="ba3d5-122">Bir gösterimini işte **parçalı** tek ve çoklu kiracı veritabanları.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="ba3d5-124">**Aralık parça eşleme**: hangi hello parça Dağıtım stratejisi temel birden çok bitişik değerleri aralığı üzerinde bir parça eşleme.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="ba3d5-125">**Başvuru tabloları**: parçalı değildir ancak parça arasında çoğaltılan tabloları.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="ba3d5-126">Örneğin, posta kodları başvuru tablosunda depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="ba3d5-127">**Parça**: parçalı bir veri kümesinden veri depolayan bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="ba3d5-128">**Parça esneklik**: her iki özelliği tooperform hello **yatay ölçekleme** ve **dikey ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="ba3d5-129">**Parçalı tabloları**: tabloları, parçalı, başka bir deyişle, verileri parçalama anahtar değerlerine göre parça dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="ba3d5-130">**Parçalama anahtar**: veri parça arasında nasıl dağıtıldığını belirler bir sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="ba3d5-131">Merhaba değer türü hello aşağıdakilerden biri olabilir: **int**, **bigint**, **varbinary**, veya **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="ba3d5-132">**Parça kümesi**: Merhaba öznitelikli toohello olan parça koleksiyonunu hello parça eşleme Yöneticisi'nde aynı parça eşleme.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="ba3d5-133">**Shardlet**: tüm hello verileri tek bir parça bir parçalama anahtar değeriyle ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="ba3d5-134">Bir shardlet hello en küçük olası veri taşıma parçalı tabloları dağıtırken birimidir.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="ba3d5-135">**Parça eşleme**: Merhaba parçalama anahtarları ve bunların ilgili parça arasındaki eşlemeleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="ba3d5-136">**Parça eşleme Yöneticisi**: hello parça harita(lar), parça konumları ve bir veya daha fazla parça kümeleri için eşlemelerini içeren bir Yönetim nesnesi ve veri deposu.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Eşlemeleri][2]

## <a name="verbs"></a><span data-ttu-id="ba3d5-138">Fiiller</span><span class="sxs-lookup"><span data-stu-id="ba3d5-138">Verbs</span></span>
<span data-ttu-id="ba3d5-139">**Yatay ölçekleme**: hello (veya) ölçeklendirme eylemi ekleyerek veya parça tooa parça eşleme, aşağıda gösterildiği gibi kaldırarak parça koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Yatay ve dikey ölçekleme][3]

<span data-ttu-id="ba3d5-141">**Birleştirme**: hello eylemi shardlets iki parça tooone parça taşıma ve uygun şekilde hello parça eşleme güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="ba3d5-142">**Shardlet taşıma**: hello act tek shardlet tooa farklı parça taşıma.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="ba3d5-143">**Parça**: yatay aynı bölümleme hello eylemi bir parçalama anahtarına göre birden çok veritabanı arasında veri yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="ba3d5-144">**Bölünmüş**: hello act birkaç shardlets bir parça tooanother (genellikle yeni) parça taşıma.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="ba3d5-145">Başlangıç noktasını Böl gibi bir parçalama anahtar hello kullanıcı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="ba3d5-146">**Dikey ölçeklendirme**: hello Yukarı (veya aşağı) ölçeklendirme eylemi hello performans düzeyini tek tek bir parça.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="ba3d5-147">Örneğin, bir parça (ve daha fazla bilgi işlem kaynakları sonuçlanır) standart tooPremium gelen değiştirme.</span><span class="sxs-lookup"><span data-stu-id="ba3d5-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

