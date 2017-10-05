---
title: "Azure olay kılavuz olay şeması"
description: "Azure olay kılavuz olan olaylar için sağlanan özellikler açıklanmaktadır."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="1f259-103">Kılavuz olay şeması</span><span class="sxs-lookup"><span data-stu-id="1f259-103">Event Grid event schema</span></span>

<span data-ttu-id="1f259-104">Bu makale, olaylar için şema ve özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f259-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="1f259-105">Olayları oluşan bir dizi beş gerekli dize özellikleri ve gerekli **veri** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1f259-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="1f259-106">Tüm olayları için herhangi bir yayımcıdan yaygın özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="1f259-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="1f259-107">**Veri** nesne her yayımcı için özel özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1f259-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="1f259-108">Sistem konuları için bu özellikleri depolama veya olay hub'ları gibi kaynak sağlayıcısı özgüdür.</span><span class="sxs-lookup"><span data-stu-id="1f259-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="1f259-109">Olayları Azure olay kılavuza birden çok olay nesneleri içeren bir dizide gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1f259-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="1f259-110">Yalnızca tek bir olay ise, dizi 1 uzunluğuna sahip.</span><span class="sxs-lookup"><span data-stu-id="1f259-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="1f259-111">Olay Özellikleri</span><span class="sxs-lookup"><span data-stu-id="1f259-111">Event properties</span></span>

<span data-ttu-id="1f259-112">Tüm olaylar aynı aşağıdaki üst düzey veri içermez.</span><span class="sxs-lookup"><span data-stu-id="1f259-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="1f259-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="1f259-113">Property</span></span> | <span data-ttu-id="1f259-114">Tür</span><span class="sxs-lookup"><span data-stu-id="1f259-114">Type</span></span> | <span data-ttu-id="1f259-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f259-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="1f259-116">Konu</span><span class="sxs-lookup"><span data-stu-id="1f259-116">topic</span></span> | <span data-ttu-id="1f259-117">Dize</span><span class="sxs-lookup"><span data-stu-id="1f259-117">string</span></span> | <span data-ttu-id="1f259-118">Olay kaynağı tam kaynak yolu.</span><span class="sxs-lookup"><span data-stu-id="1f259-118">Full resource path to the event source.</span></span> <span data-ttu-id="1f259-119">Bu alan yazılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1f259-119">This field is not writeable.</span></span> |
| <span data-ttu-id="1f259-120">Konu</span><span class="sxs-lookup"><span data-stu-id="1f259-120">subject</span></span> | <span data-ttu-id="1f259-121">Dize</span><span class="sxs-lookup"><span data-stu-id="1f259-121">string</span></span> | <span data-ttu-id="1f259-122">Yayımcı için olay konu yolu tanımlı.</span><span class="sxs-lookup"><span data-stu-id="1f259-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="1f259-123">Olay türü</span><span class="sxs-lookup"><span data-stu-id="1f259-123">eventType</span></span> | <span data-ttu-id="1f259-124">Dize</span><span class="sxs-lookup"><span data-stu-id="1f259-124">string</span></span> | <span data-ttu-id="1f259-125">Bu olay kaynağı için kayıtlı olay türünden biri.</span><span class="sxs-lookup"><span data-stu-id="1f259-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="1f259-126">EventTime</span><span class="sxs-lookup"><span data-stu-id="1f259-126">eventTime</span></span> | <span data-ttu-id="1f259-127">Dize</span><span class="sxs-lookup"><span data-stu-id="1f259-127">string</span></span> | <span data-ttu-id="1f259-128">Olayı oluşturan zaman sağlayıcının UTC zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="1f259-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="1f259-129">id</span><span class="sxs-lookup"><span data-stu-id="1f259-129">id</span></span> | <span data-ttu-id="1f259-130">Dize</span><span class="sxs-lookup"><span data-stu-id="1f259-130">string</span></span> | <span data-ttu-id="1f259-131">Olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="1f259-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="1f259-132">Veri</span><span class="sxs-lookup"><span data-stu-id="1f259-132">data</span></span> | <span data-ttu-id="1f259-133">Nesne</span><span class="sxs-lookup"><span data-stu-id="1f259-133">object</span></span> | <span data-ttu-id="1f259-134">Olay verileri kaynak sağlayıcıya özel.</span><span class="sxs-lookup"><span data-stu-id="1f259-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="1f259-135">Kullanılabilir olay kaynakları</span><span class="sxs-lookup"><span data-stu-id="1f259-135">Available event sources</span></span>

<span data-ttu-id="1f259-136">Aşağıdaki olay kaynakları olayları olay kılavuz aracılığıyla tüketim için yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="1f259-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="1f259-137">Kaynak grupları (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="1f259-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="1f259-138">Azure abonelikleri (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="1f259-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="1f259-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1f259-139">Event Hubs</span></span>
* <span data-ttu-id="1f259-140">Özel konular</span><span class="sxs-lookup"><span data-stu-id="1f259-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="1f259-141">Azure abonelikleri</span><span class="sxs-lookup"><span data-stu-id="1f259-141">Azure Subscriptions</span></span>

<span data-ttu-id="1f259-142">Azure abonelikleri şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.</span><span class="sxs-lookup"><span data-stu-id="1f259-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1f259-143">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="1f259-143">Available event types</span></span>

- <span data-ttu-id="1f259-144">**Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="1f259-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="1f259-145">**Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="1f259-146">**Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="1f259-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="1f259-147">**Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="1f259-148">**Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="1f259-149">**Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="1f259-150">Bu şablon dağıtımı iptal ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="1f259-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="1f259-151">Örnek olay şeması</span><span class="sxs-lookup"><span data-stu-id="1f259-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="1f259-152">Kaynak Grupları</span><span class="sxs-lookup"><span data-stu-id="1f259-152">Resource Groups</span></span>

<span data-ttu-id="1f259-153">Kaynak grupları şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.</span><span class="sxs-lookup"><span data-stu-id="1f259-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1f259-154">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="1f259-154">Available event types</span></span>

- <span data-ttu-id="1f259-155">**Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="1f259-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="1f259-156">**Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="1f259-157">**Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="1f259-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="1f259-158">**Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="1f259-159">**Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="1f259-160">**Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f259-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="1f259-161">Bu şablon dağıtımı iptal ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="1f259-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="1f259-162">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="1f259-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="1f259-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1f259-163">Event Hubs</span></span>

<span data-ttu-id="1f259-164">Olay hub'ları olaylardır şu anda yalnızca bir dosyayı otomatik olarak yakalama özelliğini kullanarak depoya gönderildiğinde yayılan.</span><span class="sxs-lookup"><span data-stu-id="1f259-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1f259-165">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="1f259-165">Available event types</span></span>

- <span data-ttu-id="1f259-166">**Microsoft.EventHub.CaptureFileCreated**: bir yakalama dosyası oluşturulur tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1f259-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="1f259-167">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="1f259-167">Example event</span></span>

<span data-ttu-id="1f259-168">Bu örnek olay yakalama bir dosya depoladığında gerçekleşen bir olay hub'ları olay şeması gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f259-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="1f259-169">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="1f259-169">Azure Blob Storage</span></span>

<span data-ttu-id="1f259-170">Azure Blob Storage ile özel Önizleme olay kılavuz ile tümleştirme için kaydolma.</span><span class="sxs-lookup"><span data-stu-id="1f259-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="1f259-171">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="1f259-171">Available event types</span></span>

- <span data-ttu-id="1f259-172">**Microsoft.Storage.BlobCreated**: blob oluşturulan tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1f259-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="1f259-173">**Microsoft.Storage.BlobDeleted**: blob silinmiş tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1f259-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="1f259-174">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="1f259-174">Example event</span></span>

<span data-ttu-id="1f259-175">Bu örnek olay blob oluşturulduğunda, yükseltilmiş bir depolama olay şeması gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f259-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="1f259-176">Özel konular</span><span class="sxs-lookup"><span data-stu-id="1f259-176">Custom Topics</span></span>

<span data-ttu-id="1f259-177">Özel olaylarınızı veri yükü tarafından tanımlanır ve tüm biçiminin düzgün JSON olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f259-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="1f259-178">Üst düzey veri standart kaynağı tanımlı olayları aynı alanları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="1f259-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="1f259-179">Olaylar için özel konular yayımlarken, Yönlendirme ve filtreleme yardımcı olmak üzere, olayların konu modelleme düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1f259-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="1f259-180">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="1f259-180">Example event</span></span>

<span data-ttu-id="1f259-181">Aşağıdaki örnek, özel bir konu için bir olay gösterir:</span><span class="sxs-lookup"><span data-stu-id="1f259-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="1f259-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f259-182">Next steps</span></span>

* <span data-ttu-id="1f259-183">Olay kılavuz giriş için bkz: [olay kılavuz nedir?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="1f259-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="1f259-184">Bir olay kılavuz abonelik oluşturma hakkında bilgi edinmek için [olay kılavuz abonelik şema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1f259-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
