---
title: "SQL veritabanı aaaExtended olayları | Microsoft Docs"
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
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="ac40a-103">SQL veritabanında genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="ac40a-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="ac40a-104">Bu konuda nasıl hello Azure SQL veritabanında genişletilmiş olaylar biraz farklı karşılaştırılan tooextended olayları Microsoft SQL Server'da uygulamasıdır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ac40a-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="ac40a-105">Merhaba hello genişletilmiş olaylar özelliği, SQL Database V12 Takvim 2015 yarısı ikinci kazanılan.</span><span class="sxs-lookup"><span data-stu-id="ac40a-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="ac40a-106">SQL Server 2008'den beri genişletilmiş olaylar oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="ac40a-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="ac40a-107">Merhaba özelliği SQL veritabanı üzerinde Genişletilmiş olaylar SQL Server'da hello özelliklerinin sağlam bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="ac40a-108">*Xevent'ler* 'için genişletilmiş olayları' bazen kullanılan bir resmi olmayan takma blogları ve diğer resmi olmayan konumlara adıdır.</span><span class="sxs-lookup"><span data-stu-id="ac40a-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="ac40a-109">Azure SQL Database ve Microsoft SQL Server için genişletilmiş olaylar hakkında ek bilgi şu adresten edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="ac40a-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="ac40a-110">Hızlı Başlangıç: SQL Server Genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="ac40a-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="ac40a-111">Genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="ac40a-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="ac40a-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ac40a-112">Prerequisites</span></span>

<span data-ttu-id="ac40a-113">Bu konu, zaten bazı bilgisine sahip varsayar:</span><span class="sxs-lookup"><span data-stu-id="ac40a-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="ac40a-114">[Azure SQL veritabanı hizmetinin](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ac40a-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="ac40a-115">[Olaylar Genişletilmiş](http://msdn.microsoft.com/library/bb630282.aspx) Microsoft SQL Server'da.</span><span class="sxs-lookup"><span data-stu-id="ac40a-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="ac40a-116">Belgelerimizi genişletilmiş olaylar hakkında Hello toplu tooboth SQL Server ve SQL veritabanı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="ac40a-117">Merhaba olay dosyası hello olarak seçerken aşağıdaki öğelerindeki önceki Etkilenme toohello yararlıdır [hedef](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="ac40a-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="ac40a-118">Azure depolama hizmeti</span><span class="sxs-lookup"><span data-stu-id="ac40a-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="ac40a-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac40a-119">PowerShell</span></span>
    - <span data-ttu-id="ac40a-120">[Azure Storage ile Azure PowerShell'i kullanarak](../storage/common/storage-powershell-guide-full.md) -PowerShell ve Azure Storage hizmeti hello hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac40a-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ac40a-121">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="ac40a-121">Code samples</span></span>

<span data-ttu-id="ac40a-122">İlgili Konular iki kod örnekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="ac40a-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="ac40a-123">Halka arabelleği hedef kod SQL veritabanında genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="ac40a-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="ac40a-124">Kısa basit Transact-SQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="ac40a-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="ac40a-125">Biz halka arabelleği hedefle bittiğinde, kaynaklarını alter bırak yürüterek serbest bırakmalısınız, hello kod örnek konudaki vurgulamak `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` deyimi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="ac40a-126">Halka arabelleği ile başka bir örneği daha sonra ekleyebilirsiniz `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="ac40a-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="ac40a-127">SQL veritabanı genişletilmiş olaylar için olay dosya hedef kodu</span><span class="sxs-lookup"><span data-stu-id="ac40a-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="ac40a-128">1. Aşama PowerShell toocreate bir Azure depolama kapsayıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="ac40a-129">Aşama 2 hello Azure Storage kapsayıcısını kullanan Transact-SQL ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="ac40a-130">Transact-SQL farklılıkları</span><span class="sxs-lookup"><span data-stu-id="ac40a-130">Transact-SQL differences</span></span>


- <span data-ttu-id="ac40a-131">Merhaba yürütülürken [oluşturma olay OTURUMU](http://msdn.microsoft.com/library/bb677289.aspx) hello kullandığınız SQL Server üzerinde komut **ON SERVER** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="ac40a-132">Ancak hello kullandığınız SQL veritabanındaki **ON veritabanı** yan tümcesi yerine.</span><span class="sxs-lookup"><span data-stu-id="ac40a-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="ac40a-133">Merhaba **ON veritabanı** yan tümcesi de toohello geçerlidir [ALTER olay OTURUMU](http://msdn.microsoft.com/library/bb630368.aspx) ve [bırakma olay OTURUMU](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL komutları.</span><span class="sxs-lookup"><span data-stu-id="ac40a-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="ac40a-134">Tooinclude hello olay oturumu seçeneği, en iyi uygulamadır **STARTUP_STATE ON =** içinde **oluşturma olay OTURUMU** veya **ALTER olay OTURUMU** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="ac40a-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="ac40a-135">Merhaba **ON =** değeri hello mantıksal veritabanı tooa yük devretme son yapılandırılmasına sonra otomatik yeniden başlatma destekler.</span><span class="sxs-lookup"><span data-stu-id="ac40a-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="ac40a-136">Yeni Katalog görünümleri</span><span class="sxs-lookup"><span data-stu-id="ac40a-136">New catalog views</span></span>

<span data-ttu-id="ac40a-137">Merhaba genişletilmiş olaylar özelliği birkaçı tarafından desteklenir [Katalog görünümleri](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac40a-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="ac40a-138">Katalog görünümleri hakkında size bildirmek *meta verileri veya tanımları* kullanıcı tarafından oluşturulan olay oturumlarının hello geçerli veritabanında.</span><span class="sxs-lookup"><span data-stu-id="ac40a-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="ac40a-139">Merhaba görünümleri etkin olay oturumları örnekleri hakkında bilgi döndürmeyin.</span><span class="sxs-lookup"><span data-stu-id="ac40a-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="ac40a-140">Adı</span><span class="sxs-lookup"><span data-stu-id="ac40a-140">Name of</span></span><br/><span data-ttu-id="ac40a-141">Katalog görünümü</span><span class="sxs-lookup"><span data-stu-id="ac40a-141">catalog view</span></span> | <span data-ttu-id="ac40a-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ac40a-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac40a-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="ac40a-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="ac40a-144">Her bir olay oturumu olayda her eylem için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="ac40a-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="ac40a-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="ac40a-146">Her olay için bir satır, bir olay oturumunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="ac40a-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="ac40a-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="ac40a-148">Olayları ve hedefleri açık olarak ayarlanıp özelleştirme-mümkün her sütun için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="ac40a-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="ac40a-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="ac40a-150">Her olay hedefi için bir satır için bir olay oturumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="ac40a-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="ac40a-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="ac40a-152">Her olay oturum hello SQL veritabanı veritabanında bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="ac40a-153">Microsoft SQL Server'da benzer Katalog görünümleri içeren adları sahip *klasöründe\_*  yerine *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="ac40a-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="ac40a-154">Merhaba adı deseni benzer **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="ac40a-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="ac40a-155">Yeni dinamik yönetim görünümlerini [(Dmv'leri)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac40a-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="ac40a-156">Azure SQL veritabanı sahip [dinamik yönetim görünümlerini (Dmv'leri)](http://msdn.microsoft.com/library/bb677293.aspx) genişletilmiş olaylar destekler.</span><span class="sxs-lookup"><span data-stu-id="ac40a-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="ac40a-157">Dmv'leri hakkında size bildirmek *etkin* olay oturumları.</span><span class="sxs-lookup"><span data-stu-id="ac40a-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="ac40a-158">DMV adı</span><span class="sxs-lookup"><span data-stu-id="ac40a-158">Name of DMV</span></span> | <span data-ttu-id="ac40a-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ac40a-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac40a-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="ac40a-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="ac40a-161">Olay oturumu eylemler hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="ac40a-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="ac40a-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="ac40a-163">Oturum olaylar hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-163">Returns information about session events.</span></span> |
| <span data-ttu-id="ac40a-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="ac40a-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="ac40a-165">İlişkili tooa oturum nesneleri için Hello yapılandırma değerlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="ac40a-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="ac40a-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="ac40a-167">Oturum hedefleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="ac40a-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="ac40a-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="ac40a-169">Geçerli veritabanı kapsamlı toohello her bir olay oturumu için bir satır döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac40a-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="ac40a-170">Microsoft SQL Server hello benzer Katalog görünümleri adlandırıldığı  *\_veritabanı* gibi hello kısmı adı:</span><span class="sxs-lookup"><span data-stu-id="ac40a-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="ac40a-171">**sys.dm_xe_sessions**, adı yerine</span><span class="sxs-lookup"><span data-stu-id="ac40a-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="ac40a-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="ac40a-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="ac40a-173">Dmv'leri ortak tooboth</span><span class="sxs-lookup"><span data-stu-id="ac40a-173">DMVs common tooboth</span></span>
<span data-ttu-id="ac40a-174">Genişletilmiş olaylar için ortak tooboth Azure SQL veritabanı olan ek Dmv'leri ve Microsoft SQL Server vardır:</span><span class="sxs-lookup"><span data-stu-id="ac40a-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="ac40a-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="ac40a-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="ac40a-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="ac40a-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="ac40a-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="ac40a-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="ac40a-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="ac40a-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="ac40a-179">Merhaba kullanılabilir genişletilmiş olaylar, Eylemler ve hedefleri Bul</span><span class="sxs-lookup"><span data-stu-id="ac40a-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="ac40a-180">Basit bir SQL çalıştırabilirsiniz **seçin** tooobtain hello kullanılabilir olaylar, Eylemler ve hedef listesi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

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


<span data-ttu-id="ac40a-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="ac40a-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="ac40a-182">SQL veritabanı olay oturumları için hedefleri</span><span class="sxs-lookup"><span data-stu-id="ac40a-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="ac40a-183">SQL veritabanı üzerinde olay oturumları sonuçlarından yakalayabilirsiniz hedefleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ac40a-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="ac40a-184">[Halka arabelleği hedef](http://msdn.microsoft.com/library/ff878182.aspx) -kısaca bellekte olay verileri tutar.</span><span class="sxs-lookup"><span data-stu-id="ac40a-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="ac40a-185">[Olay sayaç hedef](http://msdn.microsoft.com/library/ff878025.aspx) -genişletilmiş olaylar oturumu sırasında oluşan tüm olaylar sayar.</span><span class="sxs-lookup"><span data-stu-id="ac40a-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="ac40a-186">[Olay dosya hedef](http://msdn.microsoft.com/library/ff878115.aspx) -yazma tam arabellekleri tooan Azure depolama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ac40a-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="ac40a-187">Merhaba [olay izleme için Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API SQL veritabanı üzerinde Genişletilmiş olaylar için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ac40a-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="ac40a-188">Kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="ac40a-188">Restrictions</span></span>

<span data-ttu-id="ac40a-189">Birkaç hello bulut ortamı SQL veritabanının befitting güvenlikle ilgili farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="ac40a-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="ac40a-190">Genişletilmiş olaylar hello tek Kiracı yalıtımı model üzerinde kurulan.</span><span class="sxs-lookup"><span data-stu-id="ac40a-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="ac40a-191">Bir veritabanında bir olay oturumu başka bir veritabanından veri ve olayları erişemez.</span><span class="sxs-lookup"><span data-stu-id="ac40a-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="ac40a-192">Veremez bir **oluşturma olay OTURUMU** hello hello bağlamda deyiminin **ana** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ac40a-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="ac40a-193">İzni modeli</span><span class="sxs-lookup"><span data-stu-id="ac40a-193">Permission model</span></span>

<span data-ttu-id="ac40a-194">Sahip olmanız gerekir **denetim** hello veritabanı tooissue izninin bir **oluşturma olay OTURUMU** deyimi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="ac40a-195">Merhaba veritabanı sahibi (dbo) sahip **denetim** izni.</span><span class="sxs-lookup"><span data-stu-id="ac40a-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="ac40a-196">Depolama kapsayıcısı yetkilerini</span><span class="sxs-lookup"><span data-stu-id="ac40a-196">Storage container authorizations</span></span>

<span data-ttu-id="ac40a-197">Merhaba SAS belirteci oluşturmak için Azure depolama kapsayıcısı belirtin gerekir **rwl** hello izinleri.</span><span class="sxs-lookup"><span data-stu-id="ac40a-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="ac40a-198">Merhaba **rwl** değeri, aşağıdaki izinleri hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="ac40a-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="ac40a-199">Okuma</span><span class="sxs-lookup"><span data-stu-id="ac40a-199">Read</span></span>
- <span data-ttu-id="ac40a-200">Yazma</span><span class="sxs-lookup"><span data-stu-id="ac40a-200">Write</span></span>
- <span data-ttu-id="ac40a-201">Liste</span><span class="sxs-lookup"><span data-stu-id="ac40a-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="ac40a-202">Performansla ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="ac40a-202">Performance considerations</span></span>

<span data-ttu-id="ac40a-203">Burada genişletilmiş olaylar yoğun kullanımını birikmesini Merhaba sağlıklı olandan daha etkin bellek senaryolarda genel sistem.</span><span class="sxs-lookup"><span data-stu-id="ac40a-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="ac40a-204">Bu nedenle hello Azure SQL veritabanı sistem dinamik olarak ayarlar ve bir olay oturumu tarafından toplanabilir etkin bellek miktarını hello sınırları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ac40a-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="ac40a-205">Birçok faktöre hello dinamik hesaplama gidin.</span><span class="sxs-lookup"><span data-stu-id="ac40a-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="ac40a-206">En fazla bellek zorlanmış bildiren bir hata iletisi alırsanız, bazı düzeltici eylemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ac40a-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="ac40a-207">Daha az sayıda eşzamanlı olay oturumları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac40a-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="ac40a-208">Aracılığıyla, **oluşturma** ve **ALTER** olay oturumları için deyimleri hello hello üzerinde belirttiğiniz bellek miktarını azaltmak **MAX\_bellek** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="ac40a-209">Ağ gecikmesi</span><span class="sxs-lookup"><span data-stu-id="ac40a-209">Network latency</span></span>

<span data-ttu-id="ac40a-210">Merhaba **olay dosyası** hedef ağ gecikmesi veya Storage bloblarını kalıcı veri tooAzure sırasında hatalar deneyimi.</span><span class="sxs-lookup"><span data-stu-id="ac40a-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="ac40a-211">Merhaba ağ iletişimi toocomplete için beklerken diğer olaylar SQL veritabanında gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="ac40a-212">Bu gecikme, iş yükü yavaşlatabilir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="ac40a-213">toomitigate bu performans risk, hello ayarı kaçının **EVENT_RETENTION_MODE** çok seçenek**NO_EVENT_LOSS** olay oturumu tanımlarında.</span><span class="sxs-lookup"><span data-stu-id="ac40a-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="ac40a-214">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="ac40a-214">Related links</span></span>

- <span data-ttu-id="ac40a-215">[Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="ac40a-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="ac40a-216">Azure depolama cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="ac40a-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="ac40a-217">[Azure Storage ile Azure PowerShell'i kullanarak](../storage/common/storage-powershell-guide-full.md) -PowerShell ve Azure Storage hizmeti hello hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac40a-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="ac40a-218">Nasıl toouse Blob depolama alanından .NET</span><span class="sxs-lookup"><span data-stu-id="ac40a-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="ac40a-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ac40a-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="ac40a-220">Olay OTURUMU (Transact-SQL) oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac40a-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="ac40a-221">Microsoft SQL Server'da genişletilmiş olaylar hakkında Jonathan Kehayias blog yazılarını</span><span class="sxs-lookup"><span data-stu-id="ac40a-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="ac40a-222">Hello Azure *hizmet güncelleştirmeleri* parametresi tooAzure SQL veritabanı tarafından daraltıldığı Web sayfası:</span><span class="sxs-lookup"><span data-stu-id="ac40a-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="ac40a-223">https://Azure.microsoft.com/Updates/?Service=SQL-Database</span><span class="sxs-lookup"><span data-stu-id="ac40a-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="ac40a-224">Bağlantılar aşağıdaki hello diğer kod örnek konuları genişletilmiş olaylar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="ac40a-225">Ancak, Microsoft SQL Server Azure SQL veritabanına karşı Hello örnek hedefler olup olmadığını herhangi örnek toosee düzenli olarak denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac40a-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="ac40a-226">Ardından, küçük değişiklikler gerekli toorun hello örnek olup karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac40a-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
