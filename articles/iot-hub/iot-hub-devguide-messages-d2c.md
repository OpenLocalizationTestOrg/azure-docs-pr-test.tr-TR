---
title: "aaaUnderstand Azure IOT Hub cihaz bulut Mesajlaşma | Microsoft Docs"
description: "Geliştirici Kılavuzu - nasıl toouse cihaz IOT Hub ile Mesajlaşma buluta. Telemetri ve telemtry olmayan veri gönderme ve yönlendirme toodeliver iletileri kullanma hakkında bilgi içerir."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="445ba-104">Cihaz bulut iletilerini tooIoT Hub Gönder</span><span class="sxs-lookup"><span data-stu-id="445ba-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="445ba-105">toosend zaman serisi telemetri ve aygıtları tooyour çözüm arka ucunuz, uyarılar, aygıt tooyour IOT hub'dan cihaz bulut iletilerini gönderir.</span><span class="sxs-lookup"><span data-stu-id="445ba-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="445ba-106">IOT Hub tarafından desteklenen diğer cihaz bulut seçenekleri tartışma için bkz [cihaz bulut iletişimleri Kılavuzu][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="445ba-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="445ba-107">Bir aygıt'e yönelik uç noktası aracılığıyla cihaz bulut iletilerini gönder (**/devices/ {DeviceID} / iletileri/olayları**).</span><span class="sxs-lookup"><span data-stu-id="445ba-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="445ba-108">Yönlendirme kuralları ardından, IOT hub'ına, iletileri tooone hello service'e yönelik uç noktalar için rota.</span><span class="sxs-lookup"><span data-stu-id="445ba-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="445ba-109">Yönlendirme kuralları kullanmak hello üstbilgiler ve, hub toodetermine akan hello cihaz bulut iletilerini gövdesi nerede tooroute bunları.</span><span class="sxs-lookup"><span data-stu-id="445ba-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="445ba-110">Varsayılan olarak, iletileri yönlendirilmiş toohello yerleşik service'e yönelik uç noktası olan (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="445ba-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="445ba-111">Bu nedenle, standart kullanabilirsiniz [olay hub'ları tümleştirme ve SDK] [ lnk-compatible-endpoint] tooreceive cihaz bulut iletilerini çözümünüzdeki son yedekleme.</span><span class="sxs-lookup"><span data-stu-id="445ba-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="445ba-112">IOT Hub cihaz bulut akış Mesajlaşma düzeni kullanarak ileti uygular.</span><span class="sxs-lookup"><span data-stu-id="445ba-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="445ba-113">IOT Hub'ın cihaz bulut iletilerini gibi daha fazla [Event Hubs] [ lnk-event-hubs] *olayları* daha [Service Bus] [ lnk-servicebus] *iletileri* birden çok okuyucular tarafından okunabilir hello hizmeti aracılığıyla geçirme olayları hacmi yüksek olmasını durumunda.</span><span class="sxs-lookup"><span data-stu-id="445ba-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="445ba-114">Cihaz bulut IOT Hub ile Mesajlaşma hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="445ba-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="445ba-115">Cihaz bulut iletilerini sağlam ve bir IOT hub'ın varsayılan saklama **iletileri/olayları** tooseven günlerini uç noktası için.</span><span class="sxs-lookup"><span data-stu-id="445ba-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="445ba-116">Cihaz bulut iletilerini en fazla 256 KB olabilir ve toooptimize gönderir toplu olarak gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="445ba-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="445ba-117">Toplu işlemler en fazla 256 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="445ba-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="445ba-118">Hello açıklandığı gibi [Denetim erişim tooIoT Hub] [ lnk-devguide-security] bölüm, IOT Hub cihaz başına kimlik doğrulama ve erişim denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="445ba-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="445ba-119">IOT hub'ı too10 özel uç noktaları yukarı toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="445ba-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="445ba-120">İletiler toohello uç noktaları, IOT hub'ına yapılandırılmış yolları göre teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="445ba-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="445ba-121">Daha fazla bilgi için bkz: [yönlendirme kuralları](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="445ba-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="445ba-122">IOT Hub, milyonlarca eş zamanlı cihazı sağlar (bkz [kotalar ve azaltma][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="445ba-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="445ba-123">IOT hub'ı rasgele bölümleme izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="445ba-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="445ba-124">Cihaz bulut iletilerini bölümlenmiş kendi oluşturan bağlı **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="445ba-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="445ba-125">Merhaba hello IOT Hub ve Event Hubs Hizmetleri arasındaki farklar hakkında daha fazla bilgi için bkz: [karşılaştırma Azure IOT Hub ve Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="445ba-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="445ba-126">Telemetri olmayan trafiği Gönder</span><span class="sxs-lookup"><span data-stu-id="445ba-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="445ba-127">Genellikle, ayrıca tootelemetry veri noktaları, aygıtlar iletileri ayrı yürütme ve hello çözüm arka ucu işlemede gerektiren istekleri göndermek ve.</span><span class="sxs-lookup"><span data-stu-id="445ba-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="445ba-128">Örneğin, hello içinde belirli bir eylemi tetikleyen gereken kritik uyarılar arka uç.</span><span class="sxs-lookup"><span data-stu-id="445ba-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="445ba-129">Kolayca yazabilen bir [yönlendirme kuralı] [ lnk-devguide-custom] toosend iletileri tooan uç noktası bu tür adanmış bir ya da başlığında selamlama iletisine ya da hello ileti gövdesi bir değere göre tootheir işleme.</span><span class="sxs-lookup"><span data-stu-id="445ba-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="445ba-130">Merhaba hello en iyi şekilde tooprocess ileti bu tür hakkında daha fazla bilgi için bkz: [Öğreticisi: nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="445ba-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="445ba-131">Rota cihaz-bulut iletileri</span><span class="sxs-lookup"><span data-stu-id="445ba-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="445ba-132">Yönlendirme cihaz bulut iletilerini tooyour arka uç uygulamalar için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="445ba-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="445ba-133">Merhaba yerleşik kullanmak [Event Hub ile uyumlu uç nokta] [ lnk-compatible-endpoint] tooenable arka uç uygulamaları tooread hello cihaz bulut iletilerini hello hub tarafından alınan.</span><span class="sxs-lookup"><span data-stu-id="445ba-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="445ba-134">toolearn hello yerleşik Event Hub ile uyumlu uç noktasını hakkında bkz [hello yerleşik uç noktasından cihaz bulut iletilerini okumanızı][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="445ba-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="445ba-135">Yönlendirme kuralları toosend iletileri toocustom uç noktaları IOT hub'ınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="445ba-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="445ba-136">Olay hub'ları, Service Bus kuyruklarını veya Service Bus konu başlıklarını kullanma, arka uç uygulamaları tooread cihaz bulut iletilerini özel uç noktaları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="445ba-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="445ba-137">Yönlendirme ve özel uç noktaları hakkında toolearn bkz [özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="445ba-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="445ba-138">Yanıltma özellikleri</span><span class="sxs-lookup"><span data-stu-id="445ba-138">Anti-spoofing properties</span></span>

<span data-ttu-id="445ba-139">IOT Hub, cihaz bulut iletilerini hello aşağıdaki özelliklere tüm iletileri Damgalar yanıltma tooavoid aygıt:</span><span class="sxs-lookup"><span data-stu-id="445ba-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="445ba-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="445ba-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="445ba-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="445ba-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="445ba-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="445ba-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="445ba-143">Merhaba ilk iki hello içeren **DeviceID** ve **Generationıd** göre aygıtı kaynaklanan Merhaba, [aygıt kimlik özellikleri][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="445ba-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="445ba-144">Merhaba **ConnectionAuthMethod** özelliği hello aşağıdaki özelliklere bir JSON serileştirilmiş nesne içerir:</span><span class="sxs-lookup"><span data-stu-id="445ba-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="445ba-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="445ba-145">Next steps</span></span>

<span data-ttu-id="445ba-146">Merhaba SDK'ları hakkında bilgi için toosend cihaz bulut iletilerini kullanın, bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="445ba-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="445ba-147">Merhaba [Get Started] [ lnk-get-started] öğreticiler gösterir, sanal ve fiziksel aygıtlardan nasıl toosend cihaz-bulut iletileri.</span><span class="sxs-lookup"><span data-stu-id="445ba-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="445ba-148">Merhaba daha ayrıntılı bilgi için bkz: [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="445ba-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
