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
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="0dfc3-103">Kılavuz abonelik şeması</span><span class="sxs-lookup"><span data-stu-id="0dfc3-103">Event Grid subscription schema</span></span>

<span data-ttu-id="0dfc3-104">bir olay kılavuz abonelik toocreate, istek toohello oluşturma olay Abonelik işlem gönderin.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="0dfc3-105">Hello aşağıdaki biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="0dfc3-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="0dfc3-106">Örneğin, toocreate adlı bir depolama hesabı için bir olay aboneliği `examplestorage` bir kaynak grubunda adlı `examplegroup`, kullanım hello aşağıdaki biçim:</span><span class="sxs-lookup"><span data-stu-id="0dfc3-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="0dfc3-107">Merhaba makalede hello özellikleri ve hello hello istek gövdesi için şema açıklanır.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="0dfc3-108">Olay abonelik özellikleri</span><span class="sxs-lookup"><span data-stu-id="0dfc3-108">Event subscription properties</span></span>

| <span data-ttu-id="0dfc3-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="0dfc3-109">Property</span></span> | <span data-ttu-id="0dfc3-110">Tür</span><span class="sxs-lookup"><span data-stu-id="0dfc3-110">Type</span></span> | <span data-ttu-id="0dfc3-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dfc3-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0dfc3-112">Hedef</span><span class="sxs-lookup"><span data-stu-id="0dfc3-112">destination</span></span> | <span data-ttu-id="0dfc3-113">Nesne</span><span class="sxs-lookup"><span data-stu-id="0dfc3-113">object</span></span> | <span data-ttu-id="0dfc3-114">Merhaba uç nokta tanımlayan hello nesnesi.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="0dfc3-115">Filtre</span><span class="sxs-lookup"><span data-stu-id="0dfc3-115">filter</span></span> | <span data-ttu-id="0dfc3-116">Nesne</span><span class="sxs-lookup"><span data-stu-id="0dfc3-116">object</span></span> | <span data-ttu-id="0dfc3-117">Olay hello türleri filtrelemek için isteğe bağlı bir alan.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="0dfc3-118">hedef nesne</span><span class="sxs-lookup"><span data-stu-id="0dfc3-118">destination object</span></span>

| <span data-ttu-id="0dfc3-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="0dfc3-119">Property</span></span> | <span data-ttu-id="0dfc3-120">Tür</span><span class="sxs-lookup"><span data-stu-id="0dfc3-120">Type</span></span> | <span data-ttu-id="0dfc3-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dfc3-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0dfc3-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="0dfc3-122">endpointType</span></span> | <span data-ttu-id="0dfc3-123">Dize</span><span class="sxs-lookup"><span data-stu-id="0dfc3-123">string</span></span> | <span data-ttu-id="0dfc3-124">uç noktası hello abonelik (Web kancası/HTTP, olay hub'ı veya sıra) için Hello türü.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="0dfc3-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="0dfc3-125">endpointUrl</span></span> | <span data-ttu-id="0dfc3-126">Dize</span><span class="sxs-lookup"><span data-stu-id="0dfc3-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="0dfc3-127">filtre nesnesi</span><span class="sxs-lookup"><span data-stu-id="0dfc3-127">filter object</span></span>

| <span data-ttu-id="0dfc3-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="0dfc3-128">Property</span></span> | <span data-ttu-id="0dfc3-129">Tür</span><span class="sxs-lookup"><span data-stu-id="0dfc3-129">Type</span></span> | <span data-ttu-id="0dfc3-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dfc3-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0dfc3-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="0dfc3-131">includedEventTypes</span></span> | <span data-ttu-id="0dfc3-132">Dizi</span><span class="sxs-lookup"><span data-stu-id="0dfc3-132">array</span></span> | <span data-ttu-id="0dfc3-133">Merhaba olay türü hello Olay iletisinde bir tam eşleşme tooone bu olay türü adlarının olduğunda eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="0dfc3-134">Olay adı kayıtlı hello olay türü adları hello olay kaynağı için eşleşmediğinde bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="0dfc3-135">Varsayılan, tüm olay türleri ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-135">Default matches all event types.</span></span> |
| <span data-ttu-id="0dfc3-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="0dfc3-136">subjectBeginsWith</span></span> | <span data-ttu-id="0dfc3-137">Dize</span><span class="sxs-lookup"><span data-stu-id="0dfc3-137">string</span></span> | <span data-ttu-id="0dfc3-138">Bir önek eşleştirme filtre toohello konu alanında hello olay iletisi.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="0dfc3-139">Merhaba varsayılan ya da boş dize tüm eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="0dfc3-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="0dfc3-140">subjectEndsWith</span></span> | <span data-ttu-id="0dfc3-141">Dize</span><span class="sxs-lookup"><span data-stu-id="0dfc3-141">string</span></span> | <span data-ttu-id="0dfc3-142">Bir sonek-match filtre toohello konu alanında hello olay iletisi.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="0dfc3-143">Merhaba varsayılan ya da boş dize tüm eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="0dfc3-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="0dfc3-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="0dfc3-145">Dize</span><span class="sxs-lookup"><span data-stu-id="0dfc3-145">string</span></span> | <span data-ttu-id="0dfc3-146">Denetimler için filtreleri ile eşleşen büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="0dfc3-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="0dfc3-147">Abonelik şema örneği</span><span class="sxs-lookup"><span data-stu-id="0dfc3-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0dfc3-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dfc3-148">Next steps</span></span>

* <span data-ttu-id="0dfc3-149">Bir giriş tooEvent kılavuz için bkz: [olay kılavuz nedir?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="0dfc3-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
