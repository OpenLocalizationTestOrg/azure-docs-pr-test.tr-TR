---
title: "aaaAzure olay kılavuz teslim ve yeniden deneyin"
description: "Azure olay kılavuz olayları nasıl sunar ve teslim edilmeyen iletilerini nasıl işlediğini açıklar."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="78a78-103">Olay kılavuz ileti teslimi ve yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="78a78-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="78a78-104">Bu makalede, Azure olay kılavuz teslim edilmedi olduğunda olayları nasıl işlediğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="78a78-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="78a78-105">Olay kılavuz dayanıklı teslim sağlar.</span><span class="sxs-lookup"><span data-stu-id="78a78-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="78a78-106">Her ileti en az bir kez her abonelik için sunar.</span><span class="sxs-lookup"><span data-stu-id="78a78-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="78a78-107">Olayları hemen her abonelik kayıtlı toohello Web kancası gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78a78-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="78a78-108">Bir Web kancası olaya alınmasını kabul değil hello ilk teslimat 60 saniye içinde çalışır, olay kılavuz hello olay teslimini yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="78a78-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="78a78-109">İleti teslimat durumu</span><span class="sxs-lookup"><span data-stu-id="78a78-109">Message delivery status</span></span>

<span data-ttu-id="78a78-110">Olay kılavuz HTTP yanıt kodları tooacknowledge giriş olayların kullanır.</span><span class="sxs-lookup"><span data-stu-id="78a78-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="78a78-111">Başarı kodları</span><span class="sxs-lookup"><span data-stu-id="78a78-111">Success codes</span></span>

<span data-ttu-id="78a78-112">Merhaba aşağıdaki HTTP yanıt kodları olaya tooyour Web kancası başarıyla teslim olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="78a78-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="78a78-113">Olay kılavuz teslim tam olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="78a78-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="78a78-114">200 TAMAM</span><span class="sxs-lookup"><span data-stu-id="78a78-114">200 OK</span></span>
- <span data-ttu-id="78a78-115">202 kabul edilen</span><span class="sxs-lookup"><span data-stu-id="78a78-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="78a78-116">Hata kodları</span><span class="sxs-lookup"><span data-stu-id="78a78-116">Failure codes</span></span>

<span data-ttu-id="78a78-117">HTTP yanıt kodları aşağıdaki hello olay teslim girişimi başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="78a78-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="78a78-118">Olay kılavuz toosend hello olay yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="78a78-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="78a78-119">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="78a78-119">400 Bad Request</span></span>
- <span data-ttu-id="78a78-120">401 Yetkisiz</span><span class="sxs-lookup"><span data-stu-id="78a78-120">401 Unauthorized</span></span>
- <span data-ttu-id="78a78-121">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="78a78-121">404 Not Found</span></span>
- <span data-ttu-id="78a78-122">408 isteği zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="78a78-122">408 Request timeout</span></span>
- <span data-ttu-id="78a78-123">414 URI çok uzun</span><span class="sxs-lookup"><span data-stu-id="78a78-123">414 URI Too Long</span></span>
- <span data-ttu-id="78a78-124">500 İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="78a78-124">500 Internal Server Error</span></span>
- <span data-ttu-id="78a78-125">503 Hizmet kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="78a78-125">503 Service Unavailable</span></span>
- <span data-ttu-id="78a78-126">504 ağ geçidi zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="78a78-126">504 Gateway Timeout</span></span>

<span data-ttu-id="78a78-127">Diğer bir yanıt kodu veya bir yanıt eksikliği hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="78a78-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="78a78-128">Olay kılavuz teslim yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="78a78-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="78a78-129">Aralıkları yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="78a78-129">Retry intervals</span></span>

<span data-ttu-id="78a78-130">Olay kılavuz üstel geri alma yeniden deneme ilkesi olay teslimi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="78a78-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="78a78-131">Web kancası yanıt vermiyor veya bir hata kodu döndürüyor, zamanlama uyarınca hello Teslimde olay kılavuz yeniden deneme sayısı:</span><span class="sxs-lookup"><span data-stu-id="78a78-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="78a78-132">10 saniye</span><span class="sxs-lookup"><span data-stu-id="78a78-132">10 seconds</span></span>
2. <span data-ttu-id="78a78-133">30 saniye</span><span class="sxs-lookup"><span data-stu-id="78a78-133">30 seconds</span></span>
3. <span data-ttu-id="78a78-134">1 dakika</span><span class="sxs-lookup"><span data-stu-id="78a78-134">1 minute</span></span>
4. <span data-ttu-id="78a78-135">5 dakika</span><span class="sxs-lookup"><span data-stu-id="78a78-135">5 minutes</span></span>
5. <span data-ttu-id="78a78-136">10 dakika</span><span class="sxs-lookup"><span data-stu-id="78a78-136">10 minutes</span></span>
6. <span data-ttu-id="78a78-137">30 dakika</span><span class="sxs-lookup"><span data-stu-id="78a78-137">30 minutes</span></span>
7. <span data-ttu-id="78a78-138">1 saat</span><span class="sxs-lookup"><span data-stu-id="78a78-138">1 hour</span></span>

<span data-ttu-id="78a78-139">Olay kılavuz, küçük rasgele tooall yeniden deneme aralıkları ekler.</span><span class="sxs-lookup"><span data-stu-id="78a78-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="78a78-140">Süre yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="78a78-140">Retry duration</span></span>

<span data-ttu-id="78a78-141">Merhaba Önizleme sırasında Azure olay kılavuz iki saat içinde teslim edilmedi tüm olayları süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="78a78-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="78a78-142">Genel kullanılabilirlik önce bu kez artan too24 saatleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="78a78-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="78a78-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78a78-143">Next steps</span></span>

* <span data-ttu-id="78a78-144">Bir giriş tooEvent kılavuz için bkz: [hakkında olay kılavuz](overview.md).</span><span class="sxs-lookup"><span data-stu-id="78a78-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="78a78-145">tooquickly olay kılavuz kullanımına başlamanıza bkz [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="78a78-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
