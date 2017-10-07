---
title: "Azure SQL veritabanı kullanarak dinamik yönetim görünümlerini aaaMonitoring | Microsoft Docs"
description: "Bilgi nasıl toodetect dinamik yönetim görünümlerini toomonitor Microsoft Azure SQL veritabanı kullanarak genel performans sorunlarını tanılamak ve."
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="70c57-103">Dinamik yönetim görünümlerini kullanarak Azure SQL Database’i izleme</span><span class="sxs-lookup"><span data-stu-id="70c57-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="70c57-104">Microsoft Azure SQL veritabanı sağlar, engellenen veya uzun süre çalışan sorgular, kaynak darboğazları, zayıf sorgu planları ve benzeri tarafından kaynaklanabilir toodiagnose performans sorunlarını dinamik yönetim kümesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="70c57-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="70c57-105">Bu konu hakkında bilgi sağlar dinamik yönetim görünümlerini kullanarak toodetect ortak performans sorunları.</span><span class="sxs-lookup"><span data-stu-id="70c57-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="70c57-106">SQL veritabanı, kısmen dinamik yönetim görünümlerini üç kategoride destekler:</span><span class="sxs-lookup"><span data-stu-id="70c57-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="70c57-107">Veritabanı ile ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="70c57-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="70c57-108">Yürütme ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="70c57-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="70c57-109">İşlem ilgili dinamik yönetim görünümlerini.</span><span class="sxs-lookup"><span data-stu-id="70c57-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="70c57-110">Dinamik Yönetim görünümlerini hakkında ayrıntılı bilgi için bkz: [dinamik yönetim görünümlerini ve işlevleri (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="70c57-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="70c57-111">İzinler</span><span class="sxs-lookup"><span data-stu-id="70c57-111">Permissions</span></span>
<span data-ttu-id="70c57-112">SQL veritabanı'nda dinamik yönetim görünümünü sorgulanmasını gerektirir **görünüm veritabanı durumu** izinleri.</span><span class="sxs-lookup"><span data-stu-id="70c57-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="70c57-113">Merhaba **görünüm veritabanı durumu** izin hello geçerli veritabanının içindeki tüm nesneler hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="70c57-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="70c57-114">toogrant hello **görünüm veritabanı durumu** izin tooa belirli veritabanı kullanıcısı, sorgu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70c57-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="70c57-115">Bir şirket içi SQL Server örneğinde dinamik yönetim görünümlerini sunucu durumu bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="70c57-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="70c57-116">SQL veritabanı'nda, bunlar yalnızca geçerli, mantıksal veritabanı ile ilgili bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="70c57-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="70c57-117">Veritabanı boyutu hesaplama</span><span class="sxs-lookup"><span data-stu-id="70c57-117">Calculating database size</span></span>
<span data-ttu-id="70c57-118">Merhaba aşağıdaki sorguyu veritabanınızın (megabayt cinsinden) hello boyutunu döndürür:</span><span class="sxs-lookup"><span data-stu-id="70c57-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="70c57-119">Merhaba aşağıdaki sorguyu hello boyutu (megabayt cinsinden) tek tek nesnelerin veritabanınızda döndürür:</span><span class="sxs-lookup"><span data-stu-id="70c57-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="70c57-120">İzleme bağlantıları</span><span class="sxs-lookup"><span data-stu-id="70c57-120">Monitoring connections</span></span>
<span data-ttu-id="70c57-121">Merhaba kullanabilirsiniz [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve hello kurulan bağlantılar tooa belirli Azure SQL veritabanı sunucusu ve her bağlantının hello ayrıntıları hakkındaki bilgileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="70c57-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="70c57-122">Ayrıca, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) görünümü, tüm etkin kullanıcı bağlantıları ve iç görevler hakkında bilgi alırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="70c57-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="70c57-123">Merhaba aşağıdaki sorgu hello geçerli bağlantı üzerine bilgi alır:</span><span class="sxs-lookup"><span data-stu-id="70c57-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="70c57-124">Merhaba yürütülürken **sys.dm_exec_requests** ve **sys.dm_exec_sessions görünümleri**, varsa **görünüm veritabanı durumu** izin hello veritabanı üzerinde tüm yürütme görürsünüz. Merhaba veritabanı oturumlarını; Aksi takdirde, geçerli oturum yalnızca hello bakın.</span><span class="sxs-lookup"><span data-stu-id="70c57-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="70c57-125">Sorgu performansını izleme</span><span class="sxs-lookup"><span data-stu-id="70c57-125">Monitoring query performance</span></span>
<span data-ttu-id="70c57-126">Yavaş ya da uzun çalışan sorgu önemli sistem kaynaklarını tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="70c57-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="70c57-127">Bu bölüm, nasıl toouse dinamik yönetim toodetect birkaç ortak sorgu performans sorunlarına görünümleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="70c57-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="70c57-128">Sorun giderme, eski ancak hala yararlı bir başvuru: Merhaba [SQL Server 2008'de performans sorunlarını giderme](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet makalesi.</span><span class="sxs-lookup"><span data-stu-id="70c57-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="70c57-129">İlk N sorguları bulma</span><span class="sxs-lookup"><span data-stu-id="70c57-129">Finding top N queries</span></span>
<span data-ttu-id="70c57-130">Merhaba aşağıdaki örnek hello üst beş sorgular tarafından ortalama CPU süresi derece hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="70c57-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="70c57-131">Mantıksal olarak eşdeğer sorguları kendi toplu kaynak tüketimi gruplanması Bu örnek sorgu karma tootheir göre hello sorguları toplar.</span><span class="sxs-lookup"><span data-stu-id="70c57-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="70c57-132">Engellenen sorguları izleme</span><span class="sxs-lookup"><span data-stu-id="70c57-132">Monitoring blocked queries</span></span>
<span data-ttu-id="70c57-133">Yavaş veya uzun süre çalışan sorgular tooexcessive kaynak tüketimini katkıda ve engellenen sorguları hello sonucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="70c57-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="70c57-134">Merhaba engelleme nedeni hello sorgu planlarını kullanışlı dizinler eksikliği hello ve benzeri zayıf uygulama tasarımı, bozuk olabilir.</span><span class="sxs-lookup"><span data-stu-id="70c57-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="70c57-135">Azure SQL veritabanınızda hello sys.dm_tran_locks tooget hakkındaki bilgileri görüntüleyin hello geçerli kilitleme etkinliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70c57-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="70c57-136">Örnek kod, bkz: [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="70c57-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="70c57-137">Sorgu planları izleme</span><span class="sxs-lookup"><span data-stu-id="70c57-137">Monitoring query plans</span></span>
<span data-ttu-id="70c57-138">Verimsiz sorgu planı da CPU tüketimi artırabilir.</span><span class="sxs-lookup"><span data-stu-id="70c57-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="70c57-139">Merhaba aşağıdaki örnek kullanır hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) hangi sorgusu hello en toplam CPU kullanan toodetermine görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="70c57-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="70c57-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="70c57-140">See also</span></span>
[<span data-ttu-id="70c57-141">Giriş tooSQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="70c57-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

