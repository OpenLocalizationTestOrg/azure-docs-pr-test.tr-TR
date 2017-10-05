---
title: "Azure IOT hub'ı özel uç noktaları anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihaz bulut iletilerini özel uç noktalara yönlendirmek için yönlendirme kurallarını kullanma."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="4ec80-103">İleti yollarını ve özel uç noktaları için cihaz bulut iletilerini kullanın</span><span class="sxs-lookup"><span data-stu-id="4ec80-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="4ec80-104">IOT hub'ı etkinleştirir, yönlendirmek [cihaz bulut iletilerini] [ lnk-device-to-cloud] IOT Hub hizmeti dönük Uç noktalara ileti özelliklerine bağlı.</span><span class="sxs-lookup"><span data-stu-id="4ec80-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="4ec80-105">Yönlendirme kuralları iletilerini işlemek için ek hizmetler gerek kalmadan Git veya ek kod yazmanız gereken yeri iletileri göndermek için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ec80-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="4ec80-106">Yapılandırdığınız her yönlendirme kuralı aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4ec80-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="4ec80-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="4ec80-107">Property</span></span>      | <span data-ttu-id="4ec80-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ec80-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="4ec80-109">**Ad**</span><span class="sxs-lookup"><span data-stu-id="4ec80-109">**Name**</span></span>      | <span data-ttu-id="4ec80-110">Kural tanımlayan benzersiz adı.</span><span class="sxs-lookup"><span data-stu-id="4ec80-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="4ec80-111">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="4ec80-111">**Source**</span></span>    | <span data-ttu-id="4ec80-112">Üzerinde işlem yapılması için veri akışı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="4ec80-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="4ec80-113">Örneğin, cihaz telemetrisi.</span><span class="sxs-lookup"><span data-stu-id="4ec80-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="4ec80-114">**Koşul**</span><span class="sxs-lookup"><span data-stu-id="4ec80-114">**Condition**</span></span> | <span data-ttu-id="4ec80-115">İleti üstbilgilerini ve gövde karşı çalıştırmak ve uç nokta için bir eşleştirme olup olmadığını belirlemek için kullanılan yönlendirme kuralı için sorgu ifadesi.</span><span class="sxs-lookup"><span data-stu-id="4ec80-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="4ec80-116">Yol koşulu oluşturma hakkında daha fazla bilgi için bkz: [başvuru - cihaz çiftlerini ve işleri için sorgu dili][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="4ec80-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="4ec80-117">**Uç noktası**</span><span class="sxs-lookup"><span data-stu-id="4ec80-117">**Endpoint**</span></span>  | <span data-ttu-id="4ec80-118">Burada IOT hub'ı koşul eşleşen iletileri gönderir uç nokta adı.</span><span class="sxs-lookup"><span data-stu-id="4ec80-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="4ec80-119">Uç noktaları, IOT hub'ı ile aynı bölgede olması gerekir, aksi takdirde, çapraz bölge yazma işlemleri için ücret.</span><span class="sxs-lookup"><span data-stu-id="4ec80-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="4ec80-120">Tek bir ileti içinde durum IOT hub'ı iletiyi her eşleşen kuralla ilişkili uç teslim birden çok yönlendirme kuralları koşula eşleşmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ec80-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="4ec80-121">Tümü aynı hedefe sahip birden çok ileti eşleşirse kuralları için IOT hub'ı da otomatik olarak ileti teslimi, deduplicates, onu yalnızca bu hedefe kez yazılır.</span><span class="sxs-lookup"><span data-stu-id="4ec80-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="4ec80-122">IOT hub'ı varsayılan olan [yerleşik uç nokta][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="4ec80-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="4ec80-123">Hub'ına diğer hizmetler aboneliğinizde bağlayarak iletileri yönlendirmek için özel uç noktaları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ec80-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="4ec80-124">IOT hub'ı şu anda özel uç noktalar olarak Event Hubs, Service Bus kuyrukları ve Service Bus konu başlıklarını destekler.</span><span class="sxs-lookup"><span data-stu-id="4ec80-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="4ec80-125">Service Bus kuyrukları ve konularından ile **oturumları** veya **yinelenen saptama** etkin özel uç noktalar olarak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4ec80-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="4ec80-126">Özel uç noktaları IOT Hub oluşturma hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="4ec80-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="4ec80-127">Özel uç noktaları okuma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="4ec80-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="4ec80-128">Okuma [olay hub'ları][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="4ec80-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="4ec80-129">Okuma [Service Bus kuyruklarını][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="4ec80-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="4ec80-130">Okuma [Service Bus konu başlıklarını][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="4ec80-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="4ec80-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ec80-131">Next steps</span></span>

<span data-ttu-id="4ec80-132">IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="4ec80-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="4ec80-133">Yönlendirme kurallarını tanımlamak için kullandığınız sorgu dili hakkında daha fazla bilgi için bkz: [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="4ec80-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="4ec80-134">[Yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] öğretici yönlendirme kuralları ve özel uç noktaları nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ec80-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
