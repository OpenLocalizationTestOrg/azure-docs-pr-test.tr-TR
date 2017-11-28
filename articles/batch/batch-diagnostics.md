---
title: "aaaEnable toplu olayların - Azure günlüğe tanılama | Microsoft Docs"
description: "Kayıt ve havuzları ve görevler gibi Azure Batch hesabı kaynaklarına için tanılama günlük olayları analiz edin."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="3f432-103">Tanılama değerlendirme ve toplu çözümlerini izleme olayları günlüğe kaydedin</span><span class="sxs-lookup"><span data-stu-id="3f432-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="3f432-104">Çok sayıda Azure hizmetleriyle gibi belirli kaynaklara sırasında hello kaynak ömrü hello günlüğü olaylarını hello Batch hizmeti yayar.</span><span class="sxs-lookup"><span data-stu-id="3f432-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="3f432-105">Azure Batch tanılama günlüklerini toorecord olayları havuzları ve görevler gibi kaynaklar için etkinleştirin ve ardından hello günlükleri tanılama değerlendirme ve izleme için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f432-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="3f432-106">Havuzu gibi olaylar oluşturmak, havuzu silme, görev Başlat, görev tamamlandı ve diğerleri toplu tanılama günlüklerine eklenir.</span><span class="sxs-lookup"><span data-stu-id="3f432-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="3f432-107">Batch hesabı kaynaklarını kendileri için olayları günlüğe kaydetmeyi bu makalede ele, değil iş ve görev çıktı verileri.</span><span class="sxs-lookup"><span data-stu-id="3f432-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="3f432-108">Merhaba çıktı verilerini işler ve görevler depolama hakkında daha fazla bilgi için bkz [kalıcı Azure Batch iş ve Görev çıkış](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="3f432-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3f432-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3f432-109">Prerequisites</span></span>
* [<span data-ttu-id="3f432-110">Azure toplu işlem hesabı</span><span class="sxs-lookup"><span data-stu-id="3f432-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="3f432-111">Azure Depolama hesabınız</span><span class="sxs-lookup"><span data-stu-id="3f432-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="3f432-112">toopersist toplu tanılama günlükleri, Azure hello günlükleri depolayacağınız bir Azure Storage hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f432-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="3f432-113">Bu depolama hesabı belirtin olduğunda, [tanılama günlük kaydını etkinleştir](#enable-diagnostic-logging) Batch hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="3f432-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="3f432-114">Merhaba, belirttiğiniz günlük toplama etkinleştirdiğinizde depolama hesabı olan değil hello aynı bağlantılı depolama hesabı başvurulan tooin hello [uygulama paketleri](batch-application-packages.md) ve [görev çıktısını kalıcılığı](batch-task-output.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="3f432-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="3f432-115">Olduğunuz **ücret** Azure depolama hesabınızda depolanan hello veriler.</span><span class="sxs-lookup"><span data-stu-id="3f432-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="3f432-116">Bu makalede açıklanan hello tanılama günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3f432-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="3f432-117">Bu tasarlarken göz önünde bulundurmanız, [günlük Bekletme İlkesi](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="3f432-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="3f432-118">Tanılama günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3f432-118">Enable diagnostic logging</span></span>
<span data-ttu-id="3f432-119">Tanılama günlük varsayılan olarak, toplu işlem hesabı için etkin değil.</span><span class="sxs-lookup"><span data-stu-id="3f432-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="3f432-120">Açıkça toomonitor istediğiniz her toplu işlem hesabı için tanılama günlük kaydını etkinleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f432-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="3f432-121">Nasıl Tanılama günlüklerini tooenable koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="3f432-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="3f432-122">Merhaba tam okumanızı öneririz [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makale toogain yalnızca nasıl tooenable günlüğe kaydetme, ancak hello kategorileri oturum bir anlamak çeşitli Azure hizmetlerine hello tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3f432-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="3f432-123">Örneğin, Azure Batch tek bir günlük kategori şu anda destekler: **hizmeti günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="3f432-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="3f432-124">Hizmet Günlükleri</span><span class="sxs-lookup"><span data-stu-id="3f432-124">Service Logs</span></span>
<span data-ttu-id="3f432-125">Azure Batch hizmeti günlükleri toplu kaynak havuzu ya da görev gibi hello ömrü sırasında hello Azure Batch hizmeti tarafından oluşturulan olayları içerir.</span><span class="sxs-lookup"><span data-stu-id="3f432-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="3f432-126">Batch tarafından gösterilen her olay belirtilen hello depolanan JSON biçiminde depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="3f432-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="3f432-127">Örneğin, bu bir örnek hello gövdesi **havuzu oluşturma olayı**:</span><span class="sxs-lookup"><span data-stu-id="3f432-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="3f432-128">Her olay gövdesi bir .json bulunduğu hello dosyasında belirtilen Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="3f432-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="3f432-129">Tooaccess hello günlükleri doğrudan istiyorsanız, tooreview hello isteyebilir [tanılama günlüklerini şema hello depolama hesabındaki](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3f432-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="3f432-130">Hizmeti oturum açma olayları</span><span class="sxs-lookup"><span data-stu-id="3f432-130">Service Log events</span></span>
<span data-ttu-id="3f432-131">Merhaba Batch hizmeti şu anda hizmeti oturum açma olayları aşağıdaki hello yayar.</span><span class="sxs-lookup"><span data-stu-id="3f432-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="3f432-132">Bu makalede son güncelleştirmesinden bu yana ek olaylar eklenmemiş olabilir beri bu liste geniş kapsamlı, olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="3f432-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="3f432-133">**Hizmeti oturum açma olayları**</span><span class="sxs-lookup"><span data-stu-id="3f432-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="3f432-134">[Havuz oluşturma][pool_create]</span><span class="sxs-lookup"><span data-stu-id="3f432-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="3f432-135">[Havuzu silme Başlat][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="3f432-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="3f432-136">[Havuzu silme tamamlandı][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="3f432-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="3f432-137">[Havuzu yeniden boyutlandırma Başlat][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="3f432-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="3f432-138">[Tam havuzu yeniden boyutlandırma][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="3f432-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="3f432-139">[Görev Başlat][task_start]</span><span class="sxs-lookup"><span data-stu-id="3f432-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="3f432-140">[Görev tamamlandı][task_complete]</span><span class="sxs-lookup"><span data-stu-id="3f432-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="3f432-141">[Görev başarısız][task_fail]</span><span class="sxs-lookup"><span data-stu-id="3f432-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f432-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f432-142">Next steps</span></span>
<span data-ttu-id="3f432-143">Toplama toostoring tanılama günlük olaylarında içinde bir Azure Storage hesabı, toplu işlem hizmeti oturum açma olayları tooan da sağlanabilir [Azure olay hub'ı](../event-hubs/event-hubs-what-is-event-hubs.md)ve çok gönderme[Azure günlük analizi](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f432-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="3f432-144">Akış Azure tanılama günlükleri tooEvent hub'lar</span><span class="sxs-lookup"><span data-stu-id="3f432-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="3f432-145">Toplu iş Tanılama Olayları toohello yüksek düzeyde ölçeklenebilir bir veri alım, olay hub'ları akış.</span><span class="sxs-lookup"><span data-stu-id="3f432-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="3f432-146">Olay hub'ları sonra dönüştürmek ve tüm gerçek zamanlı analiz sağlayıcısı kullanarak depolamak saniye başına milyonlarca olayı işleyebilen.</span><span class="sxs-lookup"><span data-stu-id="3f432-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="3f432-147">Günlük analizi kullanarak Azure tanılama günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="3f432-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="3f432-148">Tanılama günlüklerini tooLog buradan hello Operations Management Suite (OMS) Portalı'nda çözümlemek, veya Power BI veya Excel'den analiz için bunları dışarı aktarmak Analytics gönderin.</span><span class="sxs-lookup"><span data-stu-id="3f432-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
