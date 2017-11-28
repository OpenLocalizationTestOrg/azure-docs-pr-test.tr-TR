---
title: "aaaAzure olay kılavuz şeması"
description: "Azure olay kılavuz olan olaylar için sağlanan hello özellikleri açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="cd4ad-103">Kılavuz olay şeması</span><span class="sxs-lookup"><span data-stu-id="cd4ad-103">Event Grid event schema</span></span>

<span data-ttu-id="cd4ad-104">Bu makalede hello özellikler ve şema olayları sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="cd4ad-105">Olayları oluşan bir dizi beş gerekli dize özellikleri ve gerekli **veri** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="cd4ad-106">Merhaba, herhangi bir yayımcıyı ortak tooall olaylarından özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="cd4ad-107">Merhaba **veri** nesne belirli tooeach yayımcı özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="cd4ad-108">Sistem için bu özellikleri depolama veya olay hub'ları gibi belirli toohello kaynak sağlayıcısı konulardır.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="cd4ad-109">Olayları tooAzure olay kılavuz birden fazla olay nesneleri içeren bir dizide gönderilir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="cd4ad-110">Yalnızca tek bir olay ise hello dizi 1 uzunluğuna sahip.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="cd4ad-111">Olay Özellikleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-111">Event properties</span></span>

<span data-ttu-id="cd4ad-112">Tüm olayları hello içerecek üst düzey veri aşağıdaki aynı.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="cd4ad-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="cd4ad-113">Property</span></span> | <span data-ttu-id="cd4ad-114">Tür</span><span class="sxs-lookup"><span data-stu-id="cd4ad-114">Type</span></span> | <span data-ttu-id="cd4ad-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cd4ad-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="cd4ad-116">Konu</span><span class="sxs-lookup"><span data-stu-id="cd4ad-116">topic</span></span> | <span data-ttu-id="cd4ad-117">Dize</span><span class="sxs-lookup"><span data-stu-id="cd4ad-117">string</span></span> | <span data-ttu-id="cd4ad-118">Tam kaynak yolu toohello olay kaynağı.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-118">Full resource path toohello event source.</span></span> <span data-ttu-id="cd4ad-119">Bu alan yazılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-119">This field is not writeable.</span></span> |
| <span data-ttu-id="cd4ad-120">Konu</span><span class="sxs-lookup"><span data-stu-id="cd4ad-120">subject</span></span> | <span data-ttu-id="cd4ad-121">Dize</span><span class="sxs-lookup"><span data-stu-id="cd4ad-121">string</span></span> | <span data-ttu-id="cd4ad-122">Yayımcı tanımlanmış bir yol toohello olay konu.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="cd4ad-123">Olay türü</span><span class="sxs-lookup"><span data-stu-id="cd4ad-123">eventType</span></span> | <span data-ttu-id="cd4ad-124">Dize</span><span class="sxs-lookup"><span data-stu-id="cd4ad-124">string</span></span> | <span data-ttu-id="cd4ad-125">Merhaba olay türleri bu olay kaynağı için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="cd4ad-126">EventTime</span><span class="sxs-lookup"><span data-stu-id="cd4ad-126">eventTime</span></span> | <span data-ttu-id="cd4ad-127">Dize</span><span class="sxs-lookup"><span data-stu-id="cd4ad-127">string</span></span> | <span data-ttu-id="cd4ad-128">Başlangıç saati hello olay hello sağlayıcının UTC zamanı temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="cd4ad-129">id</span><span class="sxs-lookup"><span data-stu-id="cd4ad-129">id</span></span> | <span data-ttu-id="cd4ad-130">Dize</span><span class="sxs-lookup"><span data-stu-id="cd4ad-130">string</span></span> | <span data-ttu-id="cd4ad-131">Merhaba olay için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="cd4ad-132">Veri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-132">data</span></span> | <span data-ttu-id="cd4ad-133">Nesne</span><span class="sxs-lookup"><span data-stu-id="cd4ad-133">object</span></span> | <span data-ttu-id="cd4ad-134">Olay verileri belirli toohello kaynak sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="cd4ad-135">Kullanılabilir olay kaynakları</span><span class="sxs-lookup"><span data-stu-id="cd4ad-135">Available event sources</span></span>

<span data-ttu-id="cd4ad-136">olay kaynakları aşağıdaki hello olayları olay kılavuz aracılığıyla tüketim için yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="cd4ad-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="cd4ad-137">Kaynak grupları (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="cd4ad-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="cd4ad-138">Azure abonelikleri (yönetim işlemlerini)</span><span class="sxs-lookup"><span data-stu-id="cd4ad-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="cd4ad-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd4ad-139">Event Hubs</span></span>
* <span data-ttu-id="cd4ad-140">Özel konular</span><span class="sxs-lookup"><span data-stu-id="cd4ad-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="cd4ad-141">Azure abonelikleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-141">Azure Subscriptions</span></span>

<span data-ttu-id="cd4ad-142">Azure abonelikleri şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="cd4ad-143">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-143">Available event types</span></span>

- <span data-ttu-id="cd4ad-144">**Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="cd4ad-145">**Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="cd4ad-146">**Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="cd4ad-147">**Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="cd4ad-148">**Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="cd4ad-149">**Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="cd4ad-150">Bu şablon dağıtımı iptal ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="cd4ad-151">Örnek olay şeması</span><span class="sxs-lookup"><span data-stu-id="cd4ad-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="cd4ad-152">Kaynak Grupları</span><span class="sxs-lookup"><span data-stu-id="cd4ad-152">Resource Groups</span></span>

<span data-ttu-id="cd4ad-153">Kaynak grupları şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="cd4ad-154">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-154">Available event types</span></span>

- <span data-ttu-id="cd4ad-155">**Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="cd4ad-156">**Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="cd4ad-157">**Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="cd4ad-158">**Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="cd4ad-159">**Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="cd4ad-160">**Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="cd4ad-161">Bu şablon dağıtımı iptal ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="cd4ad-162">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="cd4ad-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="cd4ad-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd4ad-163">Event Hubs</span></span>

<span data-ttu-id="cd4ad-164">Olay hub'ları olaylardır şu anda yalnızca bir dosya toostorage hello yakalama özelliğini kullanarak otomatik olarak gönderildiğinde yayılan.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="cd4ad-165">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-165">Available event types</span></span>

- <span data-ttu-id="cd4ad-166">**Microsoft.EventHub.CaptureFileCreated**: bir yakalama dosyası oluşturulur tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="cd4ad-167">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="cd4ad-167">Example event</span></span>

<span data-ttu-id="cd4ad-168">Bu örnek olay yakalama bir dosya depoladığında gerçekleşen bir olay hub'ları olay hello şeması gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="cd4ad-169">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="cd4ad-169">Azure Blob Storage</span></span>

<span data-ttu-id="cd4ad-170">Azure Blob Storage ile özel Önizleme olay kılavuz ile tümleştirme için kaydolma.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="cd4ad-171">Kullanılabilir olay türleri</span><span class="sxs-lookup"><span data-stu-id="cd4ad-171">Available event types</span></span>

- <span data-ttu-id="cd4ad-172">**Microsoft.Storage.BlobCreated**: blob oluşturulan tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="cd4ad-173">**Microsoft.Storage.BlobDeleted**: blob silinmiş tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="cd4ad-174">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="cd4ad-174">Example event</span></span>

<span data-ttu-id="cd4ad-175">Bu örnek olay hello şema blob oluşturulduğunda, yükseltilmiş bir depolama olayının gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="cd4ad-176">Özel konular</span><span class="sxs-lookup"><span data-stu-id="cd4ad-176">Custom Topics</span></span>

<span data-ttu-id="cd4ad-177">Özel olaylarınızı Hello veri yükünü tarafından tanımlanır ve tüm biçiminin düzgün JSON olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="cd4ad-178">Merhaba üst düzey veri hello aynı standart kaynağı tanımlı olayları olarak alanları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="cd4ad-179">Olayları toocustom konuları yayımlarken, Yönlendirme ve filtreleme, olayları tooaid hello konusunun modelleme düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="cd4ad-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="cd4ad-180">Örnek olayı</span><span class="sxs-lookup"><span data-stu-id="cd4ad-180">Example event</span></span>

<span data-ttu-id="cd4ad-181">Aşağıdaki örnek hello özel bir konu için bir olay gösterir:</span><span class="sxs-lookup"><span data-stu-id="cd4ad-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="cd4ad-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd4ad-182">Next steps</span></span>

* <span data-ttu-id="cd4ad-183">Bir giriş tooEvent kılavuz için bkz: [olay kılavuz nedir?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="cd4ad-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="cd4ad-184">bir olay kılavuz abonelik oluşturma hakkında daha fazla toolearn bkz [olay kılavuz abonelik şema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cd4ad-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
