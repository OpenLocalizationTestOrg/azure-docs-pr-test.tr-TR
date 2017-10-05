---
title: "Azure olay kılavuz abonelik şeması"
description: "Azure olay kılavuz sahip bir olay abone için özellikleri açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="0600d-103">Kılavuz abonelik şeması</span><span class="sxs-lookup"><span data-stu-id="0600d-103">Event Grid subscription schema</span></span>

<span data-ttu-id="0600d-104">Bir olay kılavuz aboneliği oluşturmak için olay oluşturma abonelik işlemi için bir istek gönderin.</span><span class="sxs-lookup"><span data-stu-id="0600d-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="0600d-105">Aşağıdaki biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="0600d-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="0600d-106">Örneğin, adında bir depolama hesabı için bir olay aboneliği oluşturmak için `examplestorage` bir kaynak grubunda adlı `examplegroup`, aşağıdaki biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="0600d-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="0600d-107">Bu makalede özellikleri ve istek gövdesi için şema anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0600d-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="0600d-108">Olay abonelik özellikleri</span><span class="sxs-lookup"><span data-stu-id="0600d-108">Event subscription properties</span></span>

| <span data-ttu-id="0600d-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="0600d-109">Property</span></span> | <span data-ttu-id="0600d-110">Tür</span><span class="sxs-lookup"><span data-stu-id="0600d-110">Type</span></span> | <span data-ttu-id="0600d-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0600d-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0600d-112">Hedef</span><span class="sxs-lookup"><span data-stu-id="0600d-112">destination</span></span> | <span data-ttu-id="0600d-113">Nesne</span><span class="sxs-lookup"><span data-stu-id="0600d-113">object</span></span> | <span data-ttu-id="0600d-114">Uç nokta tanımlayan nesnesi.</span><span class="sxs-lookup"><span data-stu-id="0600d-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="0600d-115">Filtre</span><span class="sxs-lookup"><span data-stu-id="0600d-115">filter</span></span> | <span data-ttu-id="0600d-116">Nesne</span><span class="sxs-lookup"><span data-stu-id="0600d-116">object</span></span> | <span data-ttu-id="0600d-117">Olay türlerini filtrelemek için isteğe bağlı bir alan.</span><span class="sxs-lookup"><span data-stu-id="0600d-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="0600d-118">hedef nesne</span><span class="sxs-lookup"><span data-stu-id="0600d-118">destination object</span></span>

| <span data-ttu-id="0600d-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="0600d-119">Property</span></span> | <span data-ttu-id="0600d-120">Tür</span><span class="sxs-lookup"><span data-stu-id="0600d-120">Type</span></span> | <span data-ttu-id="0600d-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0600d-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0600d-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="0600d-122">endpointType</span></span> | <span data-ttu-id="0600d-123">Dize</span><span class="sxs-lookup"><span data-stu-id="0600d-123">string</span></span> | <span data-ttu-id="0600d-124">(Web kancası/HTTP, olay hub'ı veya sıra) aboneliği için uç nokta türü.</span><span class="sxs-lookup"><span data-stu-id="0600d-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="0600d-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="0600d-125">endpointUrl</span></span> | <span data-ttu-id="0600d-126">Dize</span><span class="sxs-lookup"><span data-stu-id="0600d-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="0600d-127">filtre nesnesi</span><span class="sxs-lookup"><span data-stu-id="0600d-127">filter object</span></span>

| <span data-ttu-id="0600d-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="0600d-128">Property</span></span> | <span data-ttu-id="0600d-129">Tür</span><span class="sxs-lookup"><span data-stu-id="0600d-129">Type</span></span> | <span data-ttu-id="0600d-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0600d-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0600d-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="0600d-131">includedEventTypes</span></span> | <span data-ttu-id="0600d-132">Dizi</span><span class="sxs-lookup"><span data-stu-id="0600d-132">array</span></span> | <span data-ttu-id="0600d-133">Olay türü olay iletisini bu olay türü adları birine tam bir eşleşme eşleşmedir.</span><span class="sxs-lookup"><span data-stu-id="0600d-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="0600d-134">Olay adı için olay kaynağı kayıtlı olay türü adları eşleşmediğinde bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0600d-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="0600d-135">Varsayılan, tüm olay türleri ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0600d-135">Default matches all event types.</span></span> |
| <span data-ttu-id="0600d-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="0600d-136">subjectBeginsWith</span></span> | <span data-ttu-id="0600d-137">Dize</span><span class="sxs-lookup"><span data-stu-id="0600d-137">string</span></span> | <span data-ttu-id="0600d-138">Bir önek eşleştirme Konu alanına olay iletisi filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0600d-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="0600d-139">Varsayılan ya da boş dize tüm eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0600d-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="0600d-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="0600d-140">subjectEndsWith</span></span> | <span data-ttu-id="0600d-141">Dize</span><span class="sxs-lookup"><span data-stu-id="0600d-141">string</span></span> | <span data-ttu-id="0600d-142">Sonek eşleşme Konu alanına olay iletisi filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0600d-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="0600d-143">Varsayılan ya da boş dize tüm eşleşir.</span><span class="sxs-lookup"><span data-stu-id="0600d-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="0600d-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="0600d-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="0600d-145">Dize</span><span class="sxs-lookup"><span data-stu-id="0600d-145">string</span></span> | <span data-ttu-id="0600d-146">Denetimler için filtreleri ile eşleşen büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="0600d-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="0600d-147">Abonelik şema örneği</span><span class="sxs-lookup"><span data-stu-id="0600d-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0600d-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0600d-148">Next steps</span></span>

* <span data-ttu-id="0600d-149">Olay kılavuz giriş için bkz: [olay kılavuz nedir?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="0600d-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>