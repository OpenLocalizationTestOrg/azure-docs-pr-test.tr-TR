---
title: "Azure SQL veritabanını dinamik yönetim görünümlerini kullanarak izleme | Microsoft Docs"
description: "Algılamak ve Microsoft Azure SQL veritabanı izlemek için dinamik yönetim görünümlerini kullanarak genel performans sorunlarını tanılamak öğrenin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="86fc5-103">Dinamik yönetim görünümlerini kullanarak Azure SQL Database’i izleme</span><span class="sxs-lookup"><span data-stu-id="86fc5-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="86fc5-104">Microsoft Azure SQL veritabanı bir alt kümesini engellenen veya uzun süre çalışan sorgular, kaynak darboğazları, zayıf sorgu planları ve benzeri tarafından kaynaklanabilir performans sorunları tanılamak için dinamik yönetim görünümlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="86fc5-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="86fc5-105">Bu konu, dinamik yönetim görünümlerini kullanarak genel performans sorunlarını algılamak hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="86fc5-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="86fc5-106">SQL veritabanı, kısmen dinamik yönetim görünümlerini üç kategoride destekler:</span><span class="sxs-lookup"><span data-stu-id="86fc5-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="86fc5-107">Veritabanı ile ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="86fc5-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="86fc5-108">Yürütme ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="86fc5-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="86fc5-109">İşlem ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="86fc5-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="86fc5-110">Dinamik Yönetim görünümlerini hakkında ayrıntılı bilgi için bkz: [dinamik yönetim görünümlerini ve işlevleri (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="86fc5-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="86fc5-111">İzinler</span><span class="sxs-lookup"><span data-stu-id="86fc5-111">Permissions</span></span>
<span data-ttu-id="86fc5-112">SQL veritabanı'nda dinamik yönetim görünümünü sorgulanmasını gerektirir **görünüm veritabanı durumu** izinleri.</span><span class="sxs-lookup"><span data-stu-id="86fc5-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="86fc5-113">**Görünüm veritabanı durumu** izin geçerli veritabanının içindeki tüm nesneler hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86fc5-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="86fc5-114">Vermek için **görünüm veritabanı durumu** belirli veritabanı kullanıcı izni aşağıdaki sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="86fc5-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="86fc5-115">Bir şirket içi SQL Server örneğinde dinamik yönetim görünümlerini sunucu durumu bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="86fc5-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="86fc5-116">SQL veritabanı'nda, bunlar yalnızca geçerli, mantıksal veritabanı ile ilgili bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="86fc5-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="86fc5-117">Veritabanı boyutu hesaplama</span><span class="sxs-lookup"><span data-stu-id="86fc5-117">Calculating database size</span></span>
<span data-ttu-id="86fc5-118">Aşağıdaki sorguda (megabayt cinsinden) veritabanının boyutunu döndürür:</span><span class="sxs-lookup"><span data-stu-id="86fc5-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="86fc5-119">Aşağıdaki sorguda (megabayt cinsinden) ayrı ayrı nesneleri boyutunu veritabanınızda döndürür:</span><span class="sxs-lookup"><span data-stu-id="86fc5-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="86fc5-120">İzleme bağlantıları</span><span class="sxs-lookup"><span data-stu-id="86fc5-120">Monitoring connections</span></span>
<span data-ttu-id="86fc5-121">Kullanabileceğiniz [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) belirli bir Azure SQL veritabanı sunucusunu ve her bağlantı ayrıntıları kurulan bağlantılar hakkında bilgi almak için görünümü.</span><span class="sxs-lookup"><span data-stu-id="86fc5-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="86fc5-122">Ayrıca, [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) görünümü, tüm etkin kullanıcı bağlantıları ve iç görevler hakkında bilgi alırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="86fc5-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="86fc5-123">Aşağıdaki sorgu, geçerli bağlantı üzerine bilgi alır:</span><span class="sxs-lookup"><span data-stu-id="86fc5-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="86fc5-124">Yürütülürken **sys.dm_exec_requests** ve **sys.dm_exec_sessions görünümleri**, varsa **görünüm veritabanı durumu** izin veritabanında, tüm yürütme görürsünüz. Veritabanı oturumlarını; Aksi takdirde, yalnızca geçerli oturumu bakın.</span><span class="sxs-lookup"><span data-stu-id="86fc5-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="86fc5-125">Sorgu performansını izleme</span><span class="sxs-lookup"><span data-stu-id="86fc5-125">Monitoring query performance</span></span>
<span data-ttu-id="86fc5-126">Yavaş ya da uzun çalışan sorgu önemli sistem kaynaklarını tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="86fc5-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="86fc5-127">Bu bölüm, dinamik yönetim görünümlerini birkaç ortak sorgu performans sorunlarını algılamak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="86fc5-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="86fc5-128">Sorun giderme, eski ancak hala yararlı bir başvuru [SQL Server 2008'de performans sorunlarını giderme](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet makalesi.</span><span class="sxs-lookup"><span data-stu-id="86fc5-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="86fc5-129">İlk N sorguları bulma</span><span class="sxs-lookup"><span data-stu-id="86fc5-129">Finding top N queries</span></span>
<span data-ttu-id="86fc5-130">Aşağıdaki örnek, ortalama CPU süresi tarafından derece üst beş sorguları hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86fc5-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="86fc5-131">Mantıksal olarak eşdeğer sorguları kendi toplu kaynak tüketimi gruplanması Bu örnek sorgu karma değerlerine göre sorgular toplar.</span><span class="sxs-lookup"><span data-stu-id="86fc5-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="86fc5-132">Engellenen sorguları izleme</span><span class="sxs-lookup"><span data-stu-id="86fc5-132">Monitoring blocked queries</span></span>
<span data-ttu-id="86fc5-133">Yavaş veya uzun süre çalışan sorgular, aşırı kaynak tüketimi katkıda ve engellenen sorgu sonucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="86fc5-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="86fc5-134">Engelleme nedeni, zayıf uygulama tasarımı, hatalı sorgu planları, kullanışlı dizinler ve benzeri olmaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="86fc5-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="86fc5-135">Azure SQL veritabanınızda geçerli kilitleme etkinliği hakkında bilgi almak için sys.dm_tran_locks görünümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86fc5-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="86fc5-136">Örnek kod, bkz: [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="86fc5-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="86fc5-137">Sorgu planları izleme</span><span class="sxs-lookup"><span data-stu-id="86fc5-137">Monitoring query plans</span></span>
<span data-ttu-id="86fc5-138">Verimsiz sorgu planı da CPU tüketimi artırabilir.</span><span class="sxs-lookup"><span data-stu-id="86fc5-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="86fc5-139">Aşağıdaki örnek kullanır [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) hangi sorgusu en toplam CPU kullanan belirlemek için Görünüm.</span><span class="sxs-lookup"><span data-stu-id="86fc5-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="86fc5-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="86fc5-140">See also</span></span>
[<span data-ttu-id="86fc5-141">SQL veritabanı giriş</span><span class="sxs-lookup"><span data-stu-id="86fc5-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

