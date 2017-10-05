---
title: "Azure olay kılavuz teslim ve yeniden deneyin"
description: "Azure olay kılavuz olayları nasıl sunar ve teslim edilmeyen iletilerini nasıl işlediğini açıklar."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: e0f8afdfd84ea3c0c061459c27da285f6ae8957e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="3d60a-103">Olay kılavuz ileti teslimi ve yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="3d60a-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="3d60a-104">Bu makalede, Azure olay kılavuz teslim edilmedi olduğunda olayları nasıl işlediğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="3d60a-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="3d60a-105">Olay kılavuz dayanıklı teslim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d60a-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="3d60a-106">Her ileti en az bir kez her abonelik için sunar.</span><span class="sxs-lookup"><span data-stu-id="3d60a-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="3d60a-107">Olayları hemen her abonelik kayıtlı Web kancası için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3d60a-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="3d60a-108">Bir Web kancası ilk teslim girişiminin 60 saniye içinde bir olay alınmasını kabul değil, olay kılavuz olay teslimini yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="3d60a-108">If a webhook does not acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="3d60a-109">İleti teslimat durumu</span><span class="sxs-lookup"><span data-stu-id="3d60a-109">Message delivery status</span></span>

<span data-ttu-id="3d60a-110">Olay kılavuz HTTP yanıt kodları olayları alınmasını onaylamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d60a-110">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="3d60a-111">Başarı kodları</span><span class="sxs-lookup"><span data-stu-id="3d60a-111">Success codes</span></span>

<span data-ttu-id="3d60a-112">Aşağıdaki HTTP yanıt kodları, bir olay, Web kancası başarıyla teslim olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d60a-112">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="3d60a-113">Olay kılavuz teslim tam olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3d60a-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="3d60a-114">200 TAMAM</span><span class="sxs-lookup"><span data-stu-id="3d60a-114">200 OK</span></span>
- <span data-ttu-id="3d60a-115">202 kabul edilen</span><span class="sxs-lookup"><span data-stu-id="3d60a-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="3d60a-116">Hata kodları</span><span class="sxs-lookup"><span data-stu-id="3d60a-116">Failure codes</span></span>

<span data-ttu-id="3d60a-117">Aşağıdaki HTTP yanıt kodları, bir olay teslim girişimi başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d60a-117">The following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="3d60a-118">Olay kılavuz olay göndermek yeniden çalışır.</span><span class="sxs-lookup"><span data-stu-id="3d60a-118">Event Grid tries again to send the event.</span></span> 

- <span data-ttu-id="3d60a-119">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="3d60a-119">400 Bad Request</span></span>
- <span data-ttu-id="3d60a-120">401 Yetkisiz</span><span class="sxs-lookup"><span data-stu-id="3d60a-120">401 Unauthorized</span></span>
- <span data-ttu-id="3d60a-121">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3d60a-121">404 Not Found</span></span>
- <span data-ttu-id="3d60a-122">408 isteği zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3d60a-122">408 Request timeout</span></span>
- <span data-ttu-id="3d60a-123">414 URI çok uzun</span><span class="sxs-lookup"><span data-stu-id="3d60a-123">414 URI Too Long</span></span>
- <span data-ttu-id="3d60a-124">500 İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="3d60a-124">500 Internal Server Error</span></span>
- <span data-ttu-id="3d60a-125">503 Hizmet kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="3d60a-125">503 Service Unavailable</span></span>
- <span data-ttu-id="3d60a-126">504 ağ geçidi zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3d60a-126">504 Gateway Timeout</span></span>

<span data-ttu-id="3d60a-127">Diğer bir yanıt kodu veya bir yanıt eksikliği hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d60a-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="3d60a-128">Olay kılavuz teslim yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="3d60a-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="3d60a-129">Aralıkları yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="3d60a-129">Retry intervals</span></span>

<span data-ttu-id="3d60a-130">Olay kılavuz üstel geri alma yeniden deneme ilkesi olay teslimi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d60a-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="3d60a-131">Web kancası yanıt vermiyor veya bir hata kodu döndürüyor, olay kılavuz şu zamanlamaya göre teslim yeniden deneme:</span><span class="sxs-lookup"><span data-stu-id="3d60a-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="3d60a-132">10 saniye</span><span class="sxs-lookup"><span data-stu-id="3d60a-132">10 seconds</span></span>
2. <span data-ttu-id="3d60a-133">30 saniye</span><span class="sxs-lookup"><span data-stu-id="3d60a-133">30 seconds</span></span>
3. <span data-ttu-id="3d60a-134">1 dakika</span><span class="sxs-lookup"><span data-stu-id="3d60a-134">1 minute</span></span>
4. <span data-ttu-id="3d60a-135">5 dakika</span><span class="sxs-lookup"><span data-stu-id="3d60a-135">5 minutes</span></span>
5. <span data-ttu-id="3d60a-136">10 dakika</span><span class="sxs-lookup"><span data-stu-id="3d60a-136">10 minutes</span></span>
6. <span data-ttu-id="3d60a-137">30 dakika</span><span class="sxs-lookup"><span data-stu-id="3d60a-137">30 minutes</span></span>
7. <span data-ttu-id="3d60a-138">1 saat</span><span class="sxs-lookup"><span data-stu-id="3d60a-138">1 hour</span></span>

<span data-ttu-id="3d60a-139">Olay kılavuz, küçük rasgele tüm yeniden deneme aralıkları ekler.</span><span class="sxs-lookup"><span data-stu-id="3d60a-139">Event Grid adds a small randomization to all retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="3d60a-140">Süre yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="3d60a-140">Retry duration</span></span>

<span data-ttu-id="3d60a-141">Önizleme sırasında Azure olay kılavuz iki saat içinde teslim edilmedi tüm olayları süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="3d60a-141">During the preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="3d60a-142">Genel kullanılabilirlik önce bu süre 24 saate kadar artırılır.</span><span class="sxs-lookup"><span data-stu-id="3d60a-142">Before General Availability, this time will be increased to 24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3d60a-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d60a-143">Next steps</span></span>

* <span data-ttu-id="3d60a-144">Olay kılavuz giriş için bkz: [hakkında olay kılavuz](overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d60a-144">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="3d60a-145">Hızlı bir şekilde olay Kılavuzu ile çalışmaya başlamak için bkz: [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="3d60a-145">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>