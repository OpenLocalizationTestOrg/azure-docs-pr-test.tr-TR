---
title: "Azure Event Hubs tanılama günlüklerini | Microsoft Docs"
description: "Azure event hubs için tanılama günlükleri ayarlanacağını öğrenin."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="53684-103">Olay hub'ları tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="53684-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="53684-104">Azure Event Hubs için iki tür günlükleri görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53684-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="53684-105">**[Etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="53684-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="53684-106">Bu günlükleri bir iş üzerinde gerçekleştirilen işlemler hakkında bilgi vardır.</span><span class="sxs-lookup"><span data-stu-id="53684-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="53684-107">Günlükleri her zaman etkindir.</span><span class="sxs-lookup"><span data-stu-id="53684-107">The logs are always enabled.</span></span>
* <span data-ttu-id="53684-108">**[Tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="53684-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="53684-109">Bir işin gerçekleşen daha zengin bir görünüm her şeyin için tanılama günlükleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53684-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="53684-110">Tanılama güncelleştirmeleri ve iş çalışırken oluşan etkinlikler dahil olmak üzere iş silinene kadar işin oluşturulduğu zamandan itibaren kapak etkinlikleri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="53684-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="53684-111">Tanılama günlüklerini Aç</span><span class="sxs-lookup"><span data-stu-id="53684-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="53684-112">Tanılama günlükleri, varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="53684-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="53684-113">Tanılama günlüklerini etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="53684-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="53684-114">İçinde [Azure portal](https://portal.azure.com)altında **izleme + Yönetim**, tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="53684-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Tanılama günlüklerini dikey gezinme](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="53684-116">İzlemek istediğiniz kaynak'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="53684-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="53684-117">Tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="53684-117">Click **Turn on diagnostics**.</span></span>

    ![Tanılama günlüklerini Aç](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="53684-119">İçin **durum**, tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="53684-119">For **Status**, click **On**.</span></span>

    ![Tanılama günlüklerini durumunu değiştir](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="53684-121">İstediğiniz arşiv hedef ayarlanmış; Örneğin, bir depolama hesabı, bir olay hub'ı veya Azure günlük analizi.</span><span class="sxs-lookup"><span data-stu-id="53684-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="53684-122">Yeni tanılama ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53684-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="53684-123">Yeni ayarları yaklaşık 10 dakika içinde etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="53684-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="53684-124">Bundan sonra günlükler yapılandırılmış arşivleme hedef görünür **tanılama günlükleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="53684-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="53684-125">Tanılama yapılandırma hakkında daha fazla bilgi için bkz: [Azure tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="53684-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="53684-126">Tanılama günlüklerini kategorileri</span><span class="sxs-lookup"><span data-stu-id="53684-126">Diagnostic logs categories</span></span>
<span data-ttu-id="53684-127">Olay hub'ları iki kategorileri için tanılama günlükleri yakalar:</span><span class="sxs-lookup"><span data-stu-id="53684-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="53684-128">**ArchiveLogs**: olay hub'ları arşivler için özellikle ilgili günlükleri, hataları arşive ilgili günlükleri.</span><span class="sxs-lookup"><span data-stu-id="53684-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="53684-129">**OperationalLogs**: hakkında bilgi olay hub'ları işlemleri sırasında özellikle olmuyor işlem türü, olay hub'ı oluşturma, kullanılan kaynakları ve işlem durumu da dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="53684-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="53684-130">Tanılama günlüklerini şeması</span><span class="sxs-lookup"><span data-stu-id="53684-130">Diagnostic logs schema</span></span>
<span data-ttu-id="53684-131">Tüm günlükler JavaScript nesne gösterimi (JSON) biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="53684-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="53684-132">Her giriş aşağıdaki bölümlerde açıklanan biçimini kullanan alanlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="53684-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="53684-133">Arşiv günlükleri şeması</span><span class="sxs-lookup"><span data-stu-id="53684-133">Archive logs schema</span></span>

<span data-ttu-id="53684-134">Arşiv günlük JSON dizeler aşağıdaki tabloda listelenen öğeleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="53684-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="53684-135">Ad</span><span class="sxs-lookup"><span data-stu-id="53684-135">Name</span></span> | <span data-ttu-id="53684-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53684-136">Description</span></span>
------- | -------
<span data-ttu-id="53684-137">Görevadı</span><span class="sxs-lookup"><span data-stu-id="53684-137">TaskName</span></span> | <span data-ttu-id="53684-138">Başarısız görevi açıklaması.</span><span class="sxs-lookup"><span data-stu-id="53684-138">Description of the task that failed.</span></span>
<span data-ttu-id="53684-139">Etkinlik Kimliği</span><span class="sxs-lookup"><span data-stu-id="53684-139">ActivityId</span></span> | <span data-ttu-id="53684-140">İzleme için kullanılan iç kimliği.</span><span class="sxs-lookup"><span data-stu-id="53684-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="53684-141">İzleme kodu</span><span class="sxs-lookup"><span data-stu-id="53684-141">trackingId</span></span> | <span data-ttu-id="53684-142">İzleme için kullanılan iç kimliği.</span><span class="sxs-lookup"><span data-stu-id="53684-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="53684-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="53684-143">resourceId</span></span> | <span data-ttu-id="53684-144">Azure Resource Manager kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="53684-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="53684-145">EventHub</span><span class="sxs-lookup"><span data-stu-id="53684-145">eventHub</span></span> | <span data-ttu-id="53684-146">(Ad alanı adı dahildir) olay hub'ı tam adı.</span><span class="sxs-lookup"><span data-stu-id="53684-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="53684-147">PartitionID</span><span class="sxs-lookup"><span data-stu-id="53684-147">partitionId</span></span> | <span data-ttu-id="53684-148">Olay hub'ı üzerine yazılan bir bölüm.</span><span class="sxs-lookup"><span data-stu-id="53684-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="53684-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="53684-149">archiveStep</span></span> | <span data-ttu-id="53684-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="53684-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="53684-151">startTime</span><span class="sxs-lookup"><span data-stu-id="53684-151">startTime</span></span> | <span data-ttu-id="53684-152">Hata başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="53684-152">Failure start time.</span></span>
<span data-ttu-id="53684-153">hataları</span><span class="sxs-lookup"><span data-stu-id="53684-153">failures</span></span> | <span data-ttu-id="53684-154">Kaç kez başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="53684-154">Number of times failure occurred.</span></span>
<span data-ttu-id="53684-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="53684-155">durationInSeconds</span></span> | <span data-ttu-id="53684-156">Hatanın süresi.</span><span class="sxs-lookup"><span data-stu-id="53684-156">Duration of failure.</span></span>
<span data-ttu-id="53684-157">İleti</span><span class="sxs-lookup"><span data-stu-id="53684-157">message</span></span> | <span data-ttu-id="53684-158">Hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="53684-158">Error message.</span></span>
<span data-ttu-id="53684-159">category</span><span class="sxs-lookup"><span data-stu-id="53684-159">category</span></span> | <span data-ttu-id="53684-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="53684-160">ArchiveLogs</span></span>

<span data-ttu-id="53684-161">Aşağıdaki kod, bir arşiv günlüğü JSON dizesi örneğidir:</span><span class="sxs-lookup"><span data-stu-id="53684-161">The following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="53684-162">İşlem günlükleri şeması</span><span class="sxs-lookup"><span data-stu-id="53684-162">Operational logs schema</span></span>

<span data-ttu-id="53684-163">İşlem günlüğü JSON dizeler aşağıdaki tabloda listelenen öğeleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="53684-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="53684-164">Ad</span><span class="sxs-lookup"><span data-stu-id="53684-164">Name</span></span> | <span data-ttu-id="53684-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53684-165">Description</span></span>
------- | -------
<span data-ttu-id="53684-166">Etkinlik Kimliği</span><span class="sxs-lookup"><span data-stu-id="53684-166">ActivityId</span></span> | <span data-ttu-id="53684-167">Amaç izlemek için kullanılan iç kodu.</span><span class="sxs-lookup"><span data-stu-id="53684-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="53684-168">EventName</span><span class="sxs-lookup"><span data-stu-id="53684-168">EventName</span></span> | <span data-ttu-id="53684-169">İşlem adı.</span><span class="sxs-lookup"><span data-stu-id="53684-169">Operation name.</span></span>  
<span data-ttu-id="53684-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="53684-170">resourceId</span></span> | <span data-ttu-id="53684-171">Azure Resource Manager kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="53684-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="53684-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="53684-172">SubscriptionId</span></span> | <span data-ttu-id="53684-173">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="53684-173">Subscription ID.</span></span>
<span data-ttu-id="53684-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="53684-174">EventTimeString</span></span> | <span data-ttu-id="53684-175">İşlem süresi.</span><span class="sxs-lookup"><span data-stu-id="53684-175">Operation time.</span></span>
<span data-ttu-id="53684-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="53684-176">EventProperties</span></span> | <span data-ttu-id="53684-177">İşlem özellikleri.</span><span class="sxs-lookup"><span data-stu-id="53684-177">Operation properties.</span></span>
<span data-ttu-id="53684-178">Durum</span><span class="sxs-lookup"><span data-stu-id="53684-178">Status</span></span> | <span data-ttu-id="53684-179">İşlem durumu.</span><span class="sxs-lookup"><span data-stu-id="53684-179">Operation status.</span></span>
<span data-ttu-id="53684-180">Çağıran</span><span class="sxs-lookup"><span data-stu-id="53684-180">Caller</span></span> | <span data-ttu-id="53684-181">İşlemi (Azure portalı veya yönetim istemcisi) çağırıcı.</span><span class="sxs-lookup"><span data-stu-id="53684-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="53684-182">category</span><span class="sxs-lookup"><span data-stu-id="53684-182">category</span></span> | <span data-ttu-id="53684-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="53684-183">OperationalLogs</span></span>

<span data-ttu-id="53684-184">Aşağıdaki kod, bir işlem günlüğü JSON dizesi örneğidir:</span><span class="sxs-lookup"><span data-stu-id="53684-184">The following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="53684-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53684-185">Next steps</span></span>
* [<span data-ttu-id="53684-186">Olay hub'ları giriş</span><span class="sxs-lookup"><span data-stu-id="53684-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="53684-187">Event Hubs API’sine genel bakış</span><span class="sxs-lookup"><span data-stu-id="53684-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="53684-188">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="53684-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
