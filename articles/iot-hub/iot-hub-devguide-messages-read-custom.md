---
title: "aaaUnderstand Azure IOT hub'ı özel uç noktaları | Microsoft Docs"
description: "Geliştirici Kılavuzu - yönlendirme kullanarak tooroute cihaz bulut iletilerini toocustom uç noktaları kuralları."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="032a7-103">İleti yollarını ve özel uç noktaları için cihaz bulut iletilerini kullanın</span><span class="sxs-lookup"><span data-stu-id="032a7-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="032a7-104">IOT hub'ı etkinleştirir, tooroute [cihaz bulut iletilerini] [ lnk-device-to-cloud] tooIoT service'te Uç noktalara bağlı ileti özellikleri Hub.</span><span class="sxs-lookup"><span data-stu-id="032a7-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="032a7-105">Esneklik toosend hello kuralları verin yönlendirme hello olmadan toogo gereken yeri iletileri ek hizmetler tooprocess iletileri veya toowrite ek kod gerekir.</span><span class="sxs-lookup"><span data-stu-id="032a7-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="032a7-106">Yapılandırdığınız her yönlendirme kuralı hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="032a7-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="032a7-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="032a7-107">Property</span></span>      | <span data-ttu-id="032a7-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="032a7-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="032a7-109">**Ad**</span><span class="sxs-lookup"><span data-stu-id="032a7-109">**Name**</span></span>      | <span data-ttu-id="032a7-110">Merhaba kuralı tanımlayan hello benzersiz adı.</span><span class="sxs-lookup"><span data-stu-id="032a7-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="032a7-111">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="032a7-111">**Source**</span></span>    | <span data-ttu-id="032a7-112">Hello hello veri kaynağı üzerinde işlem toobe akış.</span><span class="sxs-lookup"><span data-stu-id="032a7-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="032a7-113">Örneğin, cihaz telemetrisi.</span><span class="sxs-lookup"><span data-stu-id="032a7-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="032a7-114">**Koşul**</span><span class="sxs-lookup"><span data-stu-id="032a7-114">**Condition**</span></span> | <span data-ttu-id="032a7-115">Merhaba ileti üstbilgilerini ve gövde karşı çalıştırmak ve hello uç noktası için bir eşleştirme olup olmadığını toodetermine kullanılan hello yönlendirme kuralı Hello sorgu ifadesi.</span><span class="sxs-lookup"><span data-stu-id="032a7-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="032a7-116">Bir yol koşulu oluşturma hakkında daha fazla bilgi için bkz: Merhaba [başvuru - cihaz çiftlerini ve işleri için sorgu dili][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="032a7-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="032a7-117">**Uç noktası**</span><span class="sxs-lookup"><span data-stu-id="032a7-117">**Endpoint**</span></span>  | <span data-ttu-id="032a7-118">Merhaba adı hello uç noktasının nereye IOT hub'ı hello koşuluyla eşleşen iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="032a7-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="032a7-119">Uç noktaları hello olmalıdır hello IOT hub'ı ile aynı bölgeye, aksi takdirde, ücret yansıtılmayacaktır çapraz bölge yazar için.</span><span class="sxs-lookup"><span data-stu-id="032a7-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="032a7-120">Tek bir ileti durumda IOT hub'ı hello ileti toohello uç nokta her eşleşen kuralla ilişkili sunan birden çok yönlendirme kuralları hello koşula eşleşmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="032a7-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="032a7-121">IOT hub'ı tüm hello sahip birden çok ileti eşleşirse kuralları için ileti teslimi, aynı zamanda otomatik olarak deduplicates aynı hedefe yalnızca yazılmış toothat hedef kez.</span><span class="sxs-lookup"><span data-stu-id="032a7-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="032a7-122">IOT hub'ı varsayılan olan [yerleşik uç nokta][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="032a7-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="032a7-123">Özel uç noktaları tooroute iletileri tooby abonelik toohello hub'ınızdaki diğer hizmetler bağlama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032a7-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="032a7-124">IOT hub'ı şu anda özel uç noktalar olarak Event Hubs, Service Bus kuyrukları ve Service Bus konu başlıklarını destekler.</span><span class="sxs-lookup"><span data-stu-id="032a7-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="032a7-125">Service Bus kuyrukları ve konularından ile **oturumları** veya **yinelenen saptama** etkin özel uç noktalar olarak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="032a7-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="032a7-126">Özel uç noktaları IOT Hub oluşturma hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="032a7-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="032a7-127">Özel uç noktaları okuma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="032a7-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="032a7-128">Okuma [olay hub'ları][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="032a7-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="032a7-129">Okuma [Service Bus kuyruklarını][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="032a7-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="032a7-130">Okuma [Service Bus konu başlıklarını][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="032a7-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="032a7-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="032a7-131">Next steps</span></span>

<span data-ttu-id="032a7-132">IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="032a7-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="032a7-133">Merhaba sorgu dili hakkında daha fazla bilgi için toodefine yönlendirme kurallarını kullanın, bkz: [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="032a7-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="032a7-134">Merhaba [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] öğretici gösterir, size, nasıl toouse yönlendirme kuralları ve özel uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="032a7-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
