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
# <a name="event-grid-event-schema"></a>Kılavuz olay şeması

Bu makale, olaylar için şema ve özellikleri sağlar. Olayları oluşan bir dizi beş gerekli dize özellikleri ve gerekli **veri** nesnesi. Tüm olayları için herhangi bir yayımcıdan yaygın özelliklerdir. **Veri** nesne her yayımcı için özel özellikleri içerir. Sistem konuları için bu özellikleri depolama veya olay hub'ları gibi kaynak sağlayıcısı özgüdür.

Olayları Azure olay kılavuza birden çok olay nesneleri içeren bir dizide gönderilir. Yalnızca tek bir olay ise, dizi 1 uzunluğuna sahip. 
 
## <a name="event-properties"></a>Olay Özellikleri

Tüm olaylar aynı aşağıdaki üst düzey veri içermez.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| Konu | Dize | Olay kaynağı tam kaynak yolu. Bu alan yazılabilir değil. |
| Konu | Dize | Yayımcı için olay konu yolu tanımlı. |
| Olay türü | Dize | Bu olay kaynağı için kayıtlı olay türünden biri. |
| EventTime | Dize | Olayı oluşturan zaman sağlayıcının UTC zamanı temel alınarak. |
| id | Dize | Olay için benzersiz tanımlayıcı. |
| Veri | Nesne | Olay verileri kaynak sağlayıcıya özel. |

## <a name="available-event-sources"></a>Kullanılabilir olay kaynakları

Aşağıdaki olay kaynakları olayları olay kılavuz aracılığıyla tüketim için yayımlayın:

* Kaynak grupları (yönetim işlemlerini)
* Azure abonelikleri (yönetim işlemlerini)
* Event Hubs
* Özel konular

## <a name="azure-subscriptions"></a>Azure abonelikleri

Azure abonelikleri şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.

### <a name="available-event-types"></a>Kullanılabilir olay türleri

- **Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.  
- **Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.  
- **Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur. Bu şablon dağıtımı iptal ortaya çıkar.

### <a name="example-event-schema"></a>Örnek olay şeması

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



## <a name="resource-groups"></a>Kaynak Grupları

Kaynak grupları şimdi VM oluşturulduğunda gibi yönetim olaylarını Azure Kaynak Yöneticisi'nden yayma veya bir depolama hesabı silinir.

### <a name="available-event-types"></a>Kullanılabilir olay türleri

- **Microsoft.Resources.ResourceWriteSuccess**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi başarılı olur.  
- **Microsoft.Resources.ResourceWriteFailure**: kaynak oluşturma veya güncelleştirme işlemi başarısız olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceWriteCancel**: yükseltilmiş ne zaman bir kaynak oluşturma veya güncelleştirme işlemi iptal edildi.  
- **Microsoft.Resources.ResourceDeleteSuccess**: kaynak silme işlemi başarılı olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceDeleteFailure**: kaynak silme işlemi başarısız olduğunda oluşturulur.  
- **Microsoft.Resources.ResourceDeleteCancel**: "kaynak silme iptal edildiğinde oluşturulur. Bu şablon dağıtımı iptal ortaya çıkar.

### <a name="example-event"></a>Örnek olayı

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



## <a name="event-hubs"></a>Event Hubs

Olay hub'ları olaylardır şu anda yalnızca bir dosyayı otomatik olarak yakalama özelliğini kullanarak depoya gönderildiğinde yayılan.

### <a name="available-event-types"></a>Kullanılabilir olay türleri

- **Microsoft.EventHub.CaptureFileCreated**: bir yakalama dosyası oluşturulur tetiklenir.

### <a name="example-event"></a>Örnek olayı

Bu örnek olay yakalama bir dosya depoladığında gerçekleşen bir olay hub'ları olay şeması gösterir. 

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



## <a name="azure-blob-storage"></a>Azure Blob Depolama

Azure Blob Storage ile özel Önizleme olay kılavuz ile tümleştirme için kaydolma.

### <a name="available-event-types"></a>Kullanılabilir olay türleri

- **Microsoft.Storage.BlobCreated**: blob oluşturulan tetiklenir.
- **Microsoft.Storage.BlobDeleted**: blob silinmiş tetiklenir.

### <a name="example-event"></a>Örnek olayı

Bu örnek olay blob oluşturulduğunda, yükseltilmiş bir depolama olay şeması gösterir. 

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




## <a name="custom-topics"></a>Özel konular

Özel olaylarınızı veri yükü tarafından tanımlanır ve tüm biçiminin düzgün JSON olabilir. Üst düzey veri standart kaynağı tanımlı olayları aynı alanları içermelidir. Olaylar için özel konular yayımlarken, Yönlendirme ve filtreleme yardımcı olmak üzere, olayların konu modelleme düşünmelisiniz.

### <a name="example-event"></a>Örnek olayı

Aşağıdaki örnek, özel bir konu için bir olay gösterir:
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

## <a name="next-steps"></a>Sonraki adımlar

* Olay kılavuz giriş için bkz: [olay kılavuz nedir?](overview.md)
* Bir olay kılavuz abonelik oluşturma hakkında bilgi edinmek için [olay kılavuz abonelik şema](subscription-creation-schema.md).
