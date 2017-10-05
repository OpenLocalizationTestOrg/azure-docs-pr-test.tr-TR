---
title: "SQL veritabanı olaylar genişletilmiş | Microsoft Docs"
description: "Azure SQL veritabanında genişletilmiş olaylar (Xevent'ler) ve nasıl olay oturumları biraz Microsoft SQL Server'ın olay oturumlarından farklılıklar açıklanmıştır."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="cf835-103">SQL veritabanında genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="cf835-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="cf835-104">Bu konuda Microsoft SQL Server Genişletilmiş olaylara göre nasıl genişletilmiş olaylar Azure SQL veritabanında biraz farklı uygulamasıdır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf835-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="cf835-105">SQL Database V12 genişletilmiş olaylar özelliği ikincide Takvim 2015 yarısı kazanılan.</span><span class="sxs-lookup"><span data-stu-id="cf835-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="cf835-106">SQL Server 2008'den beri genişletilmiş olaylar oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="cf835-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="cf835-107">SQL veritabanı üzerinde Genişletilmiş olaylar özellik kümesini sağlam bir SQL Server'ın özellikleri alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="cf835-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="cf835-108">*Xevent'ler* 'için genişletilmiş olayları' bazen kullanılan bir resmi olmayan takma blogları ve diğer resmi olmayan konumlara adıdır.</span><span class="sxs-lookup"><span data-stu-id="cf835-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="cf835-109">Azure SQL Database ve Microsoft SQL Server için genişletilmiş olaylar hakkında ek bilgi şu adresten edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="cf835-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="cf835-110">Hızlı Başlangıç: SQL Server Genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="cf835-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="cf835-111">Genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="cf835-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="cf835-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cf835-112">Prerequisites</span></span>

<span data-ttu-id="cf835-113">Bu konu, zaten bazı bilgisine sahip varsayar:</span><span class="sxs-lookup"><span data-stu-id="cf835-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="cf835-114">[Azure SQL veritabanı hizmetinin](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="cf835-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="cf835-115">[Olaylar Genişletilmiş](http://msdn.microsoft.com/library/bb630282.aspx) Microsoft SQL Server'da.</span><span class="sxs-lookup"><span data-stu-id="cf835-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="cf835-116">Belgelerimizi genişletilmiş olaylar hakkında toplu SQL Server ve SQL veritabanı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cf835-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="cf835-117">Olay dosyası olarak seçerken aşağıdaki öğeleri önceki maruz yararlıdır [hedef](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="cf835-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="cf835-118">Azure depolama hizmeti</span><span class="sxs-lookup"><span data-stu-id="cf835-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="cf835-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf835-119">PowerShell</span></span>
    - <span data-ttu-id="cf835-120">[Azure Storage ile Azure PowerShell'i kullanarak](../storage/common/storage-powershell-guide-full.md) -PowerShell ve Azure depolama hizmeti hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf835-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="cf835-121">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="cf835-121">Code samples</span></span>

<span data-ttu-id="cf835-122">İlgili Konular iki kod örnekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="cf835-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="cf835-123">Halka arabelleği hedef kod SQL veritabanında genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="cf835-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="cf835-124">Kısa basit Transact-SQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="cf835-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="cf835-125">Biz halka arabelleği hedefle bittiğinde, kaynaklarını alter bırak yürüterek serbest bırakmalısınız, kod örnek konudaki vurgulamak `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` deyimi.</span><span class="sxs-lookup"><span data-stu-id="cf835-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="cf835-126">Halka arabelleği ile başka bir örneği daha sonra ekleyebilirsiniz `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="cf835-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="cf835-127">SQL veritabanı genişletilmiş olaylar için olay dosya hedef kodu</span><span class="sxs-lookup"><span data-stu-id="cf835-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="cf835-128">1 bir Azure depolama kapsayıcısı oluşturmak için PowerShell aşamasıdır.</span><span class="sxs-lookup"><span data-stu-id="cf835-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="cf835-129">Aşama 2 Azure Storage kapsayıcısını kullanan Transact-SQL ' dir.</span><span class="sxs-lookup"><span data-stu-id="cf835-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="cf835-130">Transact-SQL farklılıkları</span><span class="sxs-lookup"><span data-stu-id="cf835-130">Transact-SQL differences</span></span>


- <span data-ttu-id="cf835-131">Çalıştırdığınızda [oluşturma olay OTURUMU](http://msdn.microsoft.com/library/bb677289.aspx) kullandığınız SQL Server üzerinde komut **ON SERVER** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="cf835-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="cf835-132">Ancak SQL veritabanında kullandığınız **ON veritabanı** yan tümcesi yerine.</span><span class="sxs-lookup"><span data-stu-id="cf835-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="cf835-133">**ON veritabanı** yan tümcesi de uygulanır [ALTER olay OTURUMU](http://msdn.microsoft.com/library/bb630368.aspx) ve [bırakma olay OTURUMU](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL komutları.</span><span class="sxs-lookup"><span data-stu-id="cf835-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="cf835-134">Olay oturumu seçeneği, dahil etmek için en iyi uygulamadır **STARTUP_STATE ON =** içinde **oluşturma olay OTURUMU** veya **ALTER olay OTURUMU** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="cf835-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="cf835-135">**ON =** değeri, bir yük devretme nedeniyle mantıksal veritabanı yapılandırılmasına sonra otomatik yeniden başlatma destekler.</span><span class="sxs-lookup"><span data-stu-id="cf835-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="cf835-136">Yeni Katalog görünümleri</span><span class="sxs-lookup"><span data-stu-id="cf835-136">New catalog views</span></span>

<span data-ttu-id="cf835-137">Genişletilmiş olaylar özelliği birkaçı tarafından desteklenir [Katalog görünümleri](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf835-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="cf835-138">Katalog görünümleri hakkında size bildirmek *meta verileri veya tanımları* kullanıcı tarafından oluşturulan olay oturumlarının geçerli veritabanında.</span><span class="sxs-lookup"><span data-stu-id="cf835-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="cf835-139">Görünümleri etkin olay oturumları örnekleri hakkında bilgi döndürmeyin.</span><span class="sxs-lookup"><span data-stu-id="cf835-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="cf835-140">Adı</span><span class="sxs-lookup"><span data-stu-id="cf835-140">Name of</span></span><br/><span data-ttu-id="cf835-141">Katalog görünümü</span><span class="sxs-lookup"><span data-stu-id="cf835-141">catalog view</span></span> | <span data-ttu-id="cf835-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf835-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf835-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="cf835-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="cf835-144">Her bir olay oturumu olayda her eylem için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="cf835-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="cf835-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="cf835-146">Her olay için bir satır, bir olay oturumunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="cf835-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="cf835-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="cf835-148">Olayları ve hedefleri açık olarak ayarlanıp özelleştirme-mümkün her sütun için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="cf835-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="cf835-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="cf835-150">Her olay hedefi için bir satır için bir olay oturumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="cf835-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="cf835-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="cf835-152">SQL veritabanı veritabanındaki her olay oturumu için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="cf835-153">Microsoft SQL Server'da benzer Katalog görünümleri içeren adları sahip *klasöründe\_*  yerine *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="cf835-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="cf835-154">Ad deseni benzer **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="cf835-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="cf835-155">Yeni dinamik yönetim görünümlerini [(Dmv'leri)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="cf835-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="cf835-156">Azure SQL veritabanı sahip [dinamik yönetim görünümlerini (Dmv'leri)](http://msdn.microsoft.com/library/bb677293.aspx) genişletilmiş olaylar destekler.</span><span class="sxs-lookup"><span data-stu-id="cf835-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="cf835-157">Dmv'leri hakkında size bildirmek *etkin* olay oturumları.</span><span class="sxs-lookup"><span data-stu-id="cf835-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="cf835-158">DMV adı</span><span class="sxs-lookup"><span data-stu-id="cf835-158">Name of DMV</span></span> | <span data-ttu-id="cf835-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf835-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf835-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="cf835-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="cf835-161">Olay oturumu eylemler hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="cf835-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="cf835-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="cf835-163">Oturum olaylar hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-163">Returns information about session events.</span></span> |
| <span data-ttu-id="cf835-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="cf835-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="cf835-165">Bir oturuma bağlı olan nesneleri için yapılandırma değerlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf835-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="cf835-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="cf835-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="cf835-167">Oturum hedefleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="cf835-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="cf835-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="cf835-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="cf835-169">Bir satır kapsamlıdır her bir olay oturumu için geçerli veritabanına döndürür.</span><span class="sxs-lookup"><span data-stu-id="cf835-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="cf835-170">Microsoft SQL Server'da benzer Katalog görünümleri olmadan adlı  *\_veritabanı* adı kısmını gibi:</span><span class="sxs-lookup"><span data-stu-id="cf835-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="cf835-171">**sys.dm_xe_sessions**, adı yerine</span><span class="sxs-lookup"><span data-stu-id="cf835-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="cf835-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="cf835-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="cf835-173">Dmv'leri ortak</span><span class="sxs-lookup"><span data-stu-id="cf835-173">DMVs common to both</span></span>
<span data-ttu-id="cf835-174">Genişletilmiş olaylar için Azure SQL Database ve Microsoft SQL Server için ortak olan ek Dmv'leri vardır:</span><span class="sxs-lookup"><span data-stu-id="cf835-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="cf835-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="cf835-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="cf835-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="cf835-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="cf835-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="cf835-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="cf835-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="cf835-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="cf835-179">Olaylar, Eylemler ve hedefleri genişletilmiş kullanılabilir Bul</span><span class="sxs-lookup"><span data-stu-id="cf835-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="cf835-180">Basit bir SQL çalıştırabilirsiniz **seçin** kullanılabilir olaylar, eylemleri ve hedef listesini elde etmek için.</span><span class="sxs-lookup"><span data-stu-id="cf835-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="cf835-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="cf835-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="cf835-182">SQL veritabanı olay oturumları için hedefleri</span><span class="sxs-lookup"><span data-stu-id="cf835-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="cf835-183">SQL veritabanı üzerinde olay oturumları sonuçlarından yakalayabilirsiniz hedefleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cf835-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="cf835-184">[Halka arabelleği hedef](http://msdn.microsoft.com/library/ff878182.aspx) -kısaca bellekte olay verileri tutar.</span><span class="sxs-lookup"><span data-stu-id="cf835-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="cf835-185">[Olay sayaç hedef](http://msdn.microsoft.com/library/ff878025.aspx) -genişletilmiş olaylar oturumu sırasında oluşan tüm olaylar sayar.</span><span class="sxs-lookup"><span data-stu-id="cf835-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="cf835-186">[Olay dosya hedef](http://msdn.microsoft.com/library/ff878115.aspx) -bir Azure depolama kapsayıcısı için tam arabellek yazar.</span><span class="sxs-lookup"><span data-stu-id="cf835-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="cf835-187">[Olay izleme için Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API SQL veritabanı üzerinde Genişletilmiş olaylar için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="cf835-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="cf835-188">Kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="cf835-188">Restrictions</span></span>

<span data-ttu-id="cf835-189">Birkaç SQL veritabanının bulut ortamı befitting güvenlikle ilgili farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="cf835-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="cf835-190">Genişletilmiş olaylar tek Kiracı yalıtımı model üzerinde kurulan.</span><span class="sxs-lookup"><span data-stu-id="cf835-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="cf835-191">Bir veritabanında bir olay oturumu başka bir veritabanından veri ve olayları erişemez.</span><span class="sxs-lookup"><span data-stu-id="cf835-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="cf835-192">Veremez bir **oluşturma olay OTURUMU** deyimi bağlamında **ana** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cf835-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="cf835-193">İzni modeli</span><span class="sxs-lookup"><span data-stu-id="cf835-193">Permission model</span></span>

<span data-ttu-id="cf835-194">Sahip olmanız gerekir **denetim** izin vermek için veritabanında bir **oluşturma olay OTURUMU** deyimi.</span><span class="sxs-lookup"><span data-stu-id="cf835-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="cf835-195">Veritabanı sahibi (dbo) sahip **denetim** izni.</span><span class="sxs-lookup"><span data-stu-id="cf835-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="cf835-196">Depolama kapsayıcısı yetkilerini</span><span class="sxs-lookup"><span data-stu-id="cf835-196">Storage container authorizations</span></span>

<span data-ttu-id="cf835-197">Azure depolama kapsayıcısının belirtmelisiniz için oluşturduğunuz SAS belirteci **rwl** izinler için.</span><span class="sxs-lookup"><span data-stu-id="cf835-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="cf835-198">**Rwl** değeri, aşağıdaki izinleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="cf835-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="cf835-199">Okuma</span><span class="sxs-lookup"><span data-stu-id="cf835-199">Read</span></span>
- <span data-ttu-id="cf835-200">Yazma</span><span class="sxs-lookup"><span data-stu-id="cf835-200">Write</span></span>
- <span data-ttu-id="cf835-201">Liste</span><span class="sxs-lookup"><span data-stu-id="cf835-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="cf835-202">Performansla ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="cf835-202">Performance considerations</span></span>

<span data-ttu-id="cf835-203">Yoğun kullanımını genişletilmiş olaylar için genel sistem sağlıklı olandan daha etkin bellek burada birikebilir senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="cf835-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="cf835-204">Bu nedenle Azure SQL veritabanı sistem dinamik olarak ayarlar ve bir olay oturumu tarafından toplanabilir etkin bellek miktarını sınırları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cf835-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="cf835-205">Birçok faktöre dinamik hesaplama gidin.</span><span class="sxs-lookup"><span data-stu-id="cf835-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="cf835-206">En fazla bellek zorlanmış bildiren bir hata iletisi alırsanız, bazı düzeltici eylemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cf835-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="cf835-207">Daha az sayıda eşzamanlı olay oturumları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cf835-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="cf835-208">Aracılığıyla, **oluşturma** ve **ALTER** deyimleri olay oturumları için sizin belirttiğiniz bellek miktarını azaltmak **MAX\_bellek** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="cf835-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="cf835-209">Ağ gecikmesi</span><span class="sxs-lookup"><span data-stu-id="cf835-209">Network latency</span></span>

<span data-ttu-id="cf835-210">**Olay dosyası** hedef ağ gecikmesi veya hatalar için Azure Storage bloblarını kalıcı veriler deneyimi.</span><span class="sxs-lookup"><span data-stu-id="cf835-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="cf835-211">SQL veritabanı diğer olaylarla tamamlamak ağ iletişimi için beklerken gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="cf835-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="cf835-212">Bu gecikme, iş yükü yavaşlatabilir.</span><span class="sxs-lookup"><span data-stu-id="cf835-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="cf835-213">Bu performans riski azaltmak için ayarı kaçının **EVENT_RETENTION_MODE** için seçenek **NO_EVENT_LOSS** olay oturumu tanımlarında.</span><span class="sxs-lookup"><span data-stu-id="cf835-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="cf835-214">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="cf835-214">Related links</span></span>

- <span data-ttu-id="cf835-215">[Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="cf835-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="cf835-216">Azure depolama cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="cf835-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="cf835-217">[Azure Storage ile Azure PowerShell'i kullanarak](../storage/common/storage-powershell-guide-full.md) -PowerShell ve Azure depolama hizmeti hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf835-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="cf835-218">BLOB depolama alanından .NET kullanma</span><span class="sxs-lookup"><span data-stu-id="cf835-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="cf835-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="cf835-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="cf835-220">Olay OTURUMU (Transact-SQL) oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf835-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="cf835-221">Microsoft SQL Server'da genişletilmiş olaylar hakkında Jonathan Kehayias blog yazılarını</span><span class="sxs-lookup"><span data-stu-id="cf835-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="cf835-222">Azure *hizmet güncelleştirmeleri* Web sayfası, Azure SQL veritabanı parametresi tarafından daraltıldığı:</span><span class="sxs-lookup"><span data-stu-id="cf835-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="cf835-223">https://Azure.microsoft.com/Updates/?Service=SQL-Database</span><span class="sxs-lookup"><span data-stu-id="cf835-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="cf835-224">Aşağıdaki bağlantılarda diğer kod örnek konuları genişletilmiş olaylar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf835-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="cf835-225">Ancak, örnek Microsoft SQL Server Azure SQL veritabanına karşı hedefler olup olmadığını görmek için herhangi bir örnek düzenli olarak denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf835-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="cf835-226">Ardından, küçük değişiklikler örneği çalıştırmak için gerekli olup olmadığını karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf835-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
