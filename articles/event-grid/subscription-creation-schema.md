---
title: "aaaAzure olay kılavuz abonelik şeması"
description: "Azure olay kılavuz abone tooan olayla Hello özelliklerini açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Kılavuz abonelik şeması

bir olay kılavuz abonelik toocreate, istek toohello oluşturma olay Abonelik işlem gönderin. Hello aşağıdaki biçimi kullanın:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Örneğin, toocreate adlı bir depolama hesabı için bir olay aboneliği `examplestorage` bir kaynak grubunda adlı `examplegroup`, kullanım hello aşağıdaki biçim:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Merhaba makalede hello özellikleri ve hello hello istek gövdesi için şema açıklanır.
 
## <a name="event-subscription-properties"></a>Olay abonelik özellikleri

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| Hedef | Nesne | Merhaba uç nokta tanımlayan hello nesnesi. |
| Filtre | Nesne | Olay hello türleri filtrelemek için isteğe bağlı bir alan. |

### <a name="destination-object"></a>hedef nesne

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| endpointType | Dize | uç noktası hello abonelik (Web kancası/HTTP, olay hub'ı veya sıra) için Hello türü. | 
| endpointUrl | Dize |  | 

### <a name="filter-object"></a>filtre nesnesi

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| includedEventTypes | Dizi | Merhaba olay türü hello Olay iletisinde bir tam eşleşme tooone bu olay türü adlarının olduğunda eşleşir. Olay adı kayıtlı hello olay türü adları hello olay kaynağı için eşleşmediğinde bir hata oluşturur. Varsayılan, tüm olay türleri ile eşleşir. |
| subjectBeginsWith | Dize | Bir önek eşleştirme filtre toohello konu alanında hello olay iletisi. Merhaba varsayılan ya da boş dize tüm eşleşir. | 
| subjectEndsWith | Dize | Bir sonek-match filtre toohello konu alanında hello olay iletisi. Merhaba varsayılan ya da boş dize tüm eşleşir. |
| subjectIsCaseSensitive | Dize | Denetimler için filtreleri ile eşleşen büyük küçük harfe duyarlı. |


## <a name="example-subscription-schema"></a>Abonelik şema örneği

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş tooEvent kılavuz için bkz: [olay kılavuz nedir?](overview.md)
