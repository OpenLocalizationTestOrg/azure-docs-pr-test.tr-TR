---
title: "T-SQL: bir Azure SQL Database esnek havuzunu yönetme | Microsoft Docs"
description: "T-SQL Azure SQL Database esnek havuzunu yönetmek için kullanın."
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
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="ff8bb-103">İzleme ve Transact-SQL sahip bir esnek havuz yönetme</span><span class="sxs-lookup"><span data-stu-id="ff8bb-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="ff8bb-104">Bu konuda nasıl yönetileceğini ölçeklenebilir gösterilmektedir [esnek havuzlar](sql-database-elastic-pool.md) Transact-SQL ile.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="ff8bb-105">Ayrıca oluşturabilir ve bir Azure esnek havuzunu yönetme [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ff8bb-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="ff8bb-106">Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="ff8bb-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="ff8bb-107">Kullanım [Create Database (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn268335.aspx) ve [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) oluşturun ve içine ve dışına esnek havuzlar veritabanlarını taşımak için komutları.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="ff8bb-108">Esnek havuz bu komutları kullanmadan önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="ff8bb-109">Bu komutlar, yalnızca veritabanları etkiler.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-109">These commands affect only databases.</span></span> <span data-ttu-id="ff8bb-110">T-SQL komutlarıyla yeni havuzları oluşturulmasını ve havuzu özelliklerini (örneğin, minimum ve maksimum Edtu) ayarı değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="ff8bb-111">Havuza alınmış bir veritabanı bir esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff8bb-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="ff8bb-112">CREATE DATABASE komutunu servıce_objectıve seçeneğiyle kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="ff8bb-113">Esnek havuzdaki tüm veritabanları esnek havuzun (temel, standart, Premium) hizmet katmanı devralır.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="ff8bb-114">Bir veritabanını esnek havuzları arasında taşıma</span><span class="sxs-lookup"><span data-stu-id="ff8bb-114">Move a database between elastic pools</span></span>
<span data-ttu-id="ff8bb-115">ALTER DATABASE komutu ile değiştir kullanın ve hizmet kümesi\_HEDEFİ seçeneği esnek olarak\_HAVUZU.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="ff8bb-116">Adı, hedef havuzunun adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="ff8bb-117">Bir veritabanını bir esnek havuza taşıma</span><span class="sxs-lookup"><span data-stu-id="ff8bb-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="ff8bb-118">ALTER DATABASE komutu ile değiştir kullanın ve hizmet kümesi\_HEDEFİ seçeneği ELASTIC_POOL olarak.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="ff8bb-119">Adı, hedef havuzunun adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="ff8bb-120">Bir veritabanını bir esnek havuz dışına taşıma</span><span class="sxs-lookup"><span data-stu-id="ff8bb-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="ff8bb-121">ALTER DATABASE komutunu kullanın ve servıce_objectıve birisi performans düzeyleri (örneğin, S0 veya S1) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="ff8bb-122">Esnek havuzdaki veritabanlarını Listele</span><span class="sxs-lookup"><span data-stu-id="ff8bb-122">List databases in an elastic pool</span></span>
<span data-ttu-id="ff8bb-123">Kullanım [sys.database\_hizmet \_hedefleri Görünüm](https://msdn.microsoft.com/library/mt712619) esnek havuzdaki tüm veritabanları listelemek için.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="ff8bb-124">Asıl veritabanı görünümü sorgulamak için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="ff8bb-125">Esnek havuz için kaynak kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="ff8bb-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="ff8bb-126">Kullanım [sys.elastic\_havuzu \_kaynak \_istatistikleri Görünüm](https://msdn.microsoft.com/library/mt280062.aspx) bir esnek havuz bir mantıksal sunucu üzerinde kaynak kullanım istatistiklerini incelemek için.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="ff8bb-127">Asıl veritabanı görünümü sorgulamak için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="ff8bb-128">Havuza alınmış bir veritabanı için kaynak kullanımını Al</span><span class="sxs-lookup"><span data-stu-id="ff8bb-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="ff8bb-129">Kullanım [sys.dm\_ db\_ kaynak\_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn800981.aspx) veya [sys.resource \_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn269979.aspx) bir veritabanında kaynak kullanım istatistiklerini incelemek için bir Esnek havuz.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="ff8bb-130">Bu işlem, kaynak kullanımı için tek bir veritabanını sorgulamak için benzer.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff8bb-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff8bb-131">Next steps</span></span>
<span data-ttu-id="ff8bb-132">Bir esnek havuz oluşturduktan sonra havuzdaki esnek veritabanları esnek iş oluşturarak yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="ff8bb-133">Esnek iş havuzdaki veritabanlarına herhangi bir sayıda karşı çalışan T-SQL betiklerini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="ff8bb-134">Daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff8bb-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="ff8bb-135">Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): ölçeğini, verileri taşımak için esnek veritabanı araçlarını kullanın sorgulamak ya da hareketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff8bb-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

