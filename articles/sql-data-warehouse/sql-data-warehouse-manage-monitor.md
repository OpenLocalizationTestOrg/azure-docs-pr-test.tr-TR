---
title: "aaaMonitor Dmv'leri kullanarak İş yükünüzün | Microsoft Docs"
description: "Bilgi nasıl toomonitor Dmv'leri kullanarak, iş yükü."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="b41dd-103">DMV’leri kullanarak iş yükünüzü izleme</span><span class="sxs-lookup"><span data-stu-id="b41dd-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="b41dd-104">Bu makalede nasıl toouse dinamik yönetim görünümlerini (Dmv'leri) toomonitor yükünüzü ve Azure SQL Data Warehouse sorgu yürütme araştırın.</span><span class="sxs-lookup"><span data-stu-id="b41dd-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="b41dd-105">İzinler</span><span class="sxs-lookup"><span data-stu-id="b41dd-105">Permissions</span></span>
<span data-ttu-id="b41dd-106">tooquery hello Dmv'leri bu makalede, görünüm veritabanı durumu veya Denetim izniniz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b41dd-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="b41dd-107">Genellikle çok daha kısıtlayıcı olduğu gibi izni veriliyor görünüm veritabanı durumu tercih edilen hello izni ' dir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="b41dd-108">İzleyici bağlantıları</span><span class="sxs-lookup"><span data-stu-id="b41dd-108">Monitor connections</span></span>
<span data-ttu-id="b41dd-109">Tüm oturumları tooSQL veri ambarı çok oturum[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="b41dd-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="b41dd-110">Bu DMV hello içeren 10.000 oturumları son.</span><span class="sxs-lookup"><span data-stu-id="b41dd-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="b41dd-111">Merhaba session_id hello birincil anahtar ve sıralı olarak her yeni oturum açma için atanır.</span><span class="sxs-lookup"><span data-stu-id="b41dd-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="b41dd-112">İzleyici sorgu yürütme</span><span class="sxs-lookup"><span data-stu-id="b41dd-112">Monitor query execution</span></span>
<span data-ttu-id="b41dd-113">SQL veri ambarı üzerinde yürütülen tüm sorguları çok günlüğe kaydedilen[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="b41dd-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="b41dd-114">Bu DMV hello içeren en son 10.000 sorgular.</span><span class="sxs-lookup"><span data-stu-id="b41dd-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="b41dd-115">Merhaba request_id benzersiz olarak her sorgu tanımlar ve bu DMV için hello birincil anahtardır.</span><span class="sxs-lookup"><span data-stu-id="b41dd-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="b41dd-116">Merhaba request_id her yeni sorgu için ardışık olarak atanır ve sorgu kimliği için anlamına gelir QID ile önek</span><span class="sxs-lookup"><span data-stu-id="b41dd-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="b41dd-117">Bu DMV verilen session_id için sorgulama belirli bir oturum açma için tüm sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="b41dd-118">Birden çok istek kimliği saklı yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b41dd-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="b41dd-119">İstek kimlikleri sıralı bir düzende atanır.</span><span class="sxs-lookup"><span data-stu-id="b41dd-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="b41dd-120">Adımları toofollow tooinvestigate sorgu yürütme planları ve belirli bir sorgu için zamanları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="b41dd-121">1. adım: tooinvestigate istediğiniz hello sorgu tanımla</span><span class="sxs-lookup"><span data-stu-id="b41dd-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="b41dd-122">Sorgu sonuçları, önceki hello gelen **Not hello istek kimliği** hello sorgunun tooinvestigate istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b41dd-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="b41dd-123">Merhaba sorgularda **askıya** durumu tooconcurrency sınırları sıraya.</span><span class="sxs-lookup"><span data-stu-id="b41dd-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="b41dd-124">Bu sorguları da hello sys.dm_pdw_waits bekler sorgu UserConcurrencyResourceType türüne sahip görünür.</span><span class="sxs-lookup"><span data-stu-id="b41dd-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="b41dd-125">Bkz: [eşzamanlılık ve iş yükü yönetimi] [ Concurrency and workload management] eşzamanlılık sınırları hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="b41dd-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="b41dd-126">Sorgular gibi başka bir nedenle nesne kilitleri için de bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b41dd-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="b41dd-127">Sorgunuz bekliyor. bir kaynak için bkz: [kaynaklar bekleniyor sorguları araştırma] [ Investigating queries waiting for resources] bu makalede daha aşağı.</span><span class="sxs-lookup"><span data-stu-id="b41dd-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="b41dd-128">toosimplify hello arama sorgusunun hello sys.dm_pdw_exec_requests tablosundaki kullanım [etiket] [ LABEL] tooassign hello sys.dm_pdw_exec_requests görünümünde aranabilir bir yorum tooyour sorgu.</span><span class="sxs-lookup"><span data-stu-id="b41dd-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="b41dd-129">2. adım: hello sorgu planı araştırın</span><span class="sxs-lookup"><span data-stu-id="b41dd-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="b41dd-130">Merhaba istek kimliği tooretrieve hello sorgunun dağıtılmış SQL (DSQL) planından kullanmak [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="b41dd-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="b41dd-131">DSQL planı beklenenden uzun sürdüğünde hello nedeni karmaşık planla birçok DSQL adımları ya da tek bir adım uzun sürüyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="b41dd-132">Merhaba planı birkaç taşıma işlemleri ile birçok adımı ise, tablo dağıtımları tooreduce veri taşıma en iyi duruma getirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b41dd-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="b41dd-133">Merhaba [Tablo dağıtımı] [ Table distribution] makalede açıklanır neden veri taşınan toosolve bir sorgu olmalı ve bazı dağıtım stratejileri toominimize veri taşımayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="b41dd-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="b41dd-134">tooinvestigate daha fazla ayrıntı tek bir adım hakkında hello *operation_type* hello uzun süre çalışan sorgu adım ve Not hello sütunu **adım dizin**:</span><span class="sxs-lookup"><span data-stu-id="b41dd-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="b41dd-135">Adım 3a devam **SQL işlemleri**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="b41dd-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="b41dd-136">Adım 3b devam **veri taşıma işlemleri**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="b41dd-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="b41dd-137">Adım 3a: Dağıtılmış hello veritabanlarını SQL araştırın</span><span class="sxs-lookup"><span data-stu-id="b41dd-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="b41dd-138">Merhaba istek kimliği ve hello adım dizin tooretrieve ayrıntılarının kullanma [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], yürütme hello sorgu adımının tüm bilgi hello içeren veritabanları dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="b41dd-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="b41dd-139">Merhaba sorgu adımı çalıştırıldığında, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] kullanılan tooretrieve hello SQL Server tahmini planından hello belirli bir çalışan hello adım için SQL Server plan önbelleğinin olabilir Dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b41dd-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="b41dd-140">Adım 3b: Dağıtılmış hello veritabanları veri taşıma araştırın</span><span class="sxs-lookup"><span data-stu-id="b41dd-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="b41dd-141">Merhaba istek kimliği ve her dağıtım noktasından çalışan bir veri taşıma adım adım dizin tooretrieve bilgilerini hello kullanma [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="b41dd-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="b41dd-142">Merhaba denetleyin *total_elapsed_time* belirli bir dağıtım diğerlerinden veri taşıma için önemli ölçüde uzun sürüyorsa sütun toosee.</span><span class="sxs-lookup"><span data-stu-id="b41dd-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="b41dd-143">Merhaba Hello uzun süre çalışan dağıtım için denetleme *rows_processed* hello bu dağıtım noktasından taşınan satır sayısını diğerlerinden daha önemli ölçüde daha büyük ise sütun toosee.</span><span class="sxs-lookup"><span data-stu-id="b41dd-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="b41dd-144">Öyleyse, bu, temel alınan verilerinizin eğme gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="b41dd-145">Merhaba sorgu çalışıyorsa, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] kullanılan tooretrieve hello SQL Server tahmini planından hello SQL adım içinde belirli bir çalışmakta hello için SQL Server plan önbelleğinin olabilir Dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b41dd-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="b41dd-146">İzleyici bekleme sorguları</span><span class="sxs-lookup"><span data-stu-id="b41dd-146">Monitor waiting queries</span></span>
<span data-ttu-id="b41dd-147">Bir kaynak için beklediğinden sorgunuzu ilerleme göstermiyor olduğunu fark ederseniz, bir sorgu için bekleyen tüm hello kaynakları gösteren bir sorgu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="b41dd-148">Merhaba sorgu başka bir sorgu kaynaklardan üzerinde bekleyen etkin olarak sonra hello durumu olacaktır **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="b41dd-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="b41dd-149">Merhaba sorgu sahip tüm gerekli hello kaynakları sonra hello durumu olacaktır **izin verildi**.</span><span class="sxs-lookup"><span data-stu-id="b41dd-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="b41dd-150">İzleyici tempdb</span><span class="sxs-lookup"><span data-stu-id="b41dd-150">Monitor tempdb</span></span>
<span data-ttu-id="b41dd-151">Yüksek tempdb kullanımı hello kök nedeni yavaş performans ve yetersiz bellek sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="b41dd-152">İlk veri eğme veya zayıf kalitesi rowgroups varsa ve hello uygun eylemleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b41dd-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="b41dd-153">Sorgu yürütme sırasında sınırlarına ulaşması tempdb bulursanız, veri ambarı ölçeklendirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b41dd-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="b41dd-154">Merhaba açıklanmıştır nasıl her düğümde sorgu başına tooidentify tempdb kullanımı.</span><span class="sxs-lookup"><span data-stu-id="b41dd-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="b41dd-155">Görünüm tooassociate hello uygun düğüm kimliği sys.dm_pdw_sql_requests için aşağıdaki hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b41dd-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="b41dd-156">Bu, tooleverage diğer geçiş Dmv'leri etkinleştir ve bu tablolarla sys.dm_pdw_sql_requests katılın.</span><span class="sxs-lookup"><span data-stu-id="b41dd-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="b41dd-157">Sorgu toomonitor tempdb aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b41dd-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="b41dd-158">İzleyici bellek</span><span class="sxs-lookup"><span data-stu-id="b41dd-158">Monitor memory</span></span>

<span data-ttu-id="b41dd-159">Bellek hello kök nedeni yavaş performans ve yetersiz bellek sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b41dd-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="b41dd-160">İlk veri eğme veya zayıf kalitesi rowgroups varsa ve hello uygun eylemleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b41dd-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="b41dd-161">SQL Server bellek kullanımı sorgu yürütme sırasında sınırlarına ulaşması bulursanız, veri ambarı ölçeklendirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b41dd-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="b41dd-162">Sorgu aşağıdaki hello düğüm başına SQL Server bellek kullanımı ve bellek baskısı döndürür:</span><span class="sxs-lookup"><span data-stu-id="b41dd-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="b41dd-163">İzleyici işlem günlüğü boyutu</span><span class="sxs-lookup"><span data-stu-id="b41dd-163">Monitor transaction log size</span></span>
<span data-ttu-id="b41dd-164">Merhaba aşağıdaki sorguyu hello işlem günlüğü boyutu her dağıtım noktasında döndürür.</span><span class="sxs-lookup"><span data-stu-id="b41dd-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="b41dd-165">Veri eğme veya zayıf kalitesi rowgroups varsa ve hello uygun eylemleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b41dd-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="b41dd-166">Merhaba günlük dosyalarından birini 160 GB ulaşıyor varsa, örnek, ölçeklendirme veya işlem boyutunuz sınırlama düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b41dd-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="b41dd-167">İzleme işlemi günlük geri alma</span><span class="sxs-lookup"><span data-stu-id="b41dd-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="b41dd-168">Sorgularınızın başarısız veya uzun süre tooproceed alma, denetleyin ve geri alma işlemler varsa izleyin.</span><span class="sxs-lookup"><span data-stu-id="b41dd-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="b41dd-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b41dd-169">Next steps</span></span>
<span data-ttu-id="b41dd-170">Bkz: [sistem görünümleri] [ System views] Dmv'leri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b41dd-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="b41dd-171">Bkz: [SQL veri ambarı en iyi yöntemler] [ SQL Data Warehouse best practices] en iyi uygulamalar hakkında daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="b41dd-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
