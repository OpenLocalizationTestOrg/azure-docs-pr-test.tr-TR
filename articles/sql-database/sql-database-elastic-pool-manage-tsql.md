---
title: "T-SQL: bir Azure SQL Database esnek havuzunu yönetme | Microsoft Docs"
description: "T-SQL toomanage bir Azure SQL Database esnek havuzunu kullanın."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="b26a8-103">İzleme ve Transact-SQL sahip bir esnek havuz yönetme</span><span class="sxs-lookup"><span data-stu-id="b26a8-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="b26a8-104">Bu konu, nasıl gösterir toomanage ölçeklenebilir [esnek havuzlar](sql-database-elastic-pool.md) Transact-SQL ile.</span><span class="sxs-lookup"><span data-stu-id="b26a8-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="b26a8-105">Ayrıca oluşturmak ve bir Azure esnek havuz hello yönetmek [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello veya [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b26a8-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="b26a8-106">Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="b26a8-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="b26a8-107">Kullanım hello [Create Database (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn268335.aspx) ve [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) toocreate ve taşıma veritabanları içine ve dışına esnek havuzlar komutları.</span><span class="sxs-lookup"><span data-stu-id="b26a8-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="b26a8-108">Bu komutlar kullanmadan önce hello esnek havuz mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b26a8-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="b26a8-109">Bu komutlar, yalnızca veritabanları etkiler.</span><span class="sxs-lookup"><span data-stu-id="b26a8-109">These commands affect only databases.</span></span> <span data-ttu-id="b26a8-110">Yeni havuzları oluşturulmasını ve hello ayarı (örneğin, minimum ve maksimum Edtu) havuzu özelliklerinin T-SQL komutlarıyla değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="b26a8-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="b26a8-111">Havuza alınmış bir veritabanı bir esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="b26a8-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="b26a8-112">Merhaba servıce_objectıve seçeneği ile Merhaba CREATE DATABASE komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="b26a8-113">Esnek havuzdaki tüm veritabanları hello hizmet katmanı hello esnek havuzun (temel, standart, Premium) devralır.</span><span class="sxs-lookup"><span data-stu-id="b26a8-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="b26a8-114">Bir veritabanını esnek havuzları arasında taşıma</span><span class="sxs-lookup"><span data-stu-id="b26a8-114">Move a database between elastic pools</span></span>
<span data-ttu-id="b26a8-115">Merhaba Değiştir ile Merhaba ALTER DATABASE komutunu kullanın ve hizmet kümesi\_HEDEFİ seçeneği esnek olarak\_HAVUZU.</span><span class="sxs-lookup"><span data-stu-id="b26a8-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="b26a8-116">Merhaba adı toohello hello hedef havuzu adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="b26a8-117">Bir veritabanını bir esnek havuza taşıma</span><span class="sxs-lookup"><span data-stu-id="b26a8-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="b26a8-118">Merhaba Değiştir ile Merhaba ALTER DATABASE komutunu kullanın ve hizmet kümesi\_HEDEFİ seçeneği ELASTIC_POOL olarak.</span><span class="sxs-lookup"><span data-stu-id="b26a8-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="b26a8-119">Merhaba adı toohello hello hedef havuzu adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="b26a8-120">Bir veritabanını bir esnek havuz dışına taşıma</span><span class="sxs-lookup"><span data-stu-id="b26a8-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="b26a8-121">Merhaba ALTER DATABASE komutunu kullanın ve hello servıce_objectıve tooone hello performans düzeyleri (örneğin, S0 veya S1) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="b26a8-122">Esnek havuzdaki veritabanlarını Listele</span><span class="sxs-lookup"><span data-stu-id="b26a8-122">List databases in an elastic pool</span></span>
<span data-ttu-id="b26a8-123">Kullanım hello [sys.database\_hizmet \_hedefleri Görünüm](https://msdn.microsoft.com/library/mt712619) toolist tüm esnek havuzdaki veritabanları hello.</span><span class="sxs-lookup"><span data-stu-id="b26a8-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="b26a8-124">Toohello asıl veritabanı tooquery hello görünümü oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="b26a8-125">Esnek havuz için kaynak kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="b26a8-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="b26a8-126">Kullanım hello [sys.elastic\_havuzu \_kaynak \_istatistikleri Görünüm](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello kaynak kullanım istatistiklerini bir esnek havuz bir mantıksal sunucu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="b26a8-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="b26a8-127">Toohello asıl veritabanı tooquery hello görünümü oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b26a8-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="b26a8-128">Havuza alınmış bir veritabanı için kaynak kullanımını Al</span><span class="sxs-lookup"><span data-stu-id="b26a8-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="b26a8-129">Kullanım hello [sys.dm\_ db\_ kaynak\_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn800981.aspx) veya [sys.resource \_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello kaynak kullanım istatistiklerini bir Esnek havuzdaki veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b26a8-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="b26a8-130">Tek veritabanı için benzer tooquerying kaynak kullanımı işlemidir.</span><span class="sxs-lookup"><span data-stu-id="b26a8-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b26a8-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b26a8-131">Next steps</span></span>
<span data-ttu-id="b26a8-132">Bir esnek havuz oluşturduktan sonra esnek iş oluşturarak hello havuzdaki esnek veritabanları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b26a8-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="b26a8-133">Esnek iş hello havuzdaki veritabanları herhangi bir sayıda karşı çalışan T-SQL betiklerini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b26a8-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="b26a8-134">Daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b26a8-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="b26a8-135">Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): esnek veritabanı araçlarını tooscale çıkışı kullanın, veri taşıma sorgulamak ya da hareketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b26a8-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

