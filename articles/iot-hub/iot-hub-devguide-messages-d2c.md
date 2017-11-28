---
title: "Azure IOT Hub cihaz bulut Mesajlaşma anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - IOT Hub ile cihaz bulut Mesajlaşma kullanma. Telemetri ve telemtry olmayan veri gönderme ve iletileri sunmak için yönlendirmeyi kullanma hakkında bilgiler içerir."
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
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="bd292-104">IOT hub'a cihaz-bulut iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="bd292-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="bd292-105">Zaman serisi telemetri ve uyarılar, çözüm arka ucuna cihazlarınızdan göndermek için cihaz bulut iletilerini cihazınızın IOT hub'ınıza gönderin.</span><span class="sxs-lookup"><span data-stu-id="bd292-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="bd292-106">IOT Hub tarafından desteklenen diğer cihaz bulut seçenekleri tartışma için bkz [cihaz bulut iletişimleri Kılavuzu][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="bd292-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="bd292-107">Bir aygıt'e yönelik uç noktası aracılığıyla cihaz bulut iletilerini gönder (**/devices/ {DeviceID} / iletileri/olayları**).</span><span class="sxs-lookup"><span data-stu-id="bd292-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="bd292-108">Yönlendirme kuralları ardından, IOT hub'ındaki service'e yönelik uç noktalardan biri iletilerinizi rotaya.</span><span class="sxs-lookup"><span data-stu-id="bd292-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="bd292-109">Yönlendirme kuralları, onları yönlendirmek nereye belirlemek için üstbilgiler ve hub'ınız akan cihaz bulut iletilerini gövdesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd292-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="bd292-110">Varsayılan olarak, yerleşik service'e yönelik uç noktasına iletileri yönlendirilir (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="bd292-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="bd292-111">Bu nedenle, standart kullanabilirsiniz [olay hub'ları tümleştirme ve SDK] [ lnk-compatible-endpoint] çözüm arka ucu cihaz-bulut iletileri almak için.</span><span class="sxs-lookup"><span data-stu-id="bd292-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="bd292-112">IOT Hub cihaz bulut akış Mesajlaşma düzeni kullanarak ileti uygular.</span><span class="sxs-lookup"><span data-stu-id="bd292-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="bd292-113">IOT Hub'ın cihaz bulut iletilerini gibi daha fazla [Event Hubs] [ lnk-event-hubs] *olayları* daha [Service Bus] [ lnk-servicebus] *iletileri* birden çok okuyucular tarafından okunabilir hizmeti aracılığıyla geçirme olayları hacmi yüksek olmasını durumunda.</span><span class="sxs-lookup"><span data-stu-id="bd292-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="bd292-114">Cihaz bulut IOT Hub ile Mesajlaşma aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="bd292-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="bd292-115">Cihaz bulut iletilerini sağlam ve bir IOT hub'ın varsayılan saklama **iletileri/olayları** endpoint yedi gündür.</span><span class="sxs-lookup"><span data-stu-id="bd292-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="bd292-116">Cihaz bulut iletilerini en fazla 256 KB olabilir ve gönderir iyileştirmek için toplu olarak gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bd292-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="bd292-117">Toplu işlemler en fazla 256 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd292-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="bd292-118">İçinde anlatıldığı gibi [IOT Hub'ına erişim denetim] [ lnk-devguide-security] bölüm, IOT Hub cihaz başına kimlik doğrulama ve erişim denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd292-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="bd292-119">IOT Hub, en fazla 10 özel uç noktaları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd292-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="bd292-120">İletiler, IOT hub'ına yapılandırılmış yolları göre Uç noktalara teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="bd292-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="bd292-121">Daha fazla bilgi için bkz: [yönlendirme kuralları](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="bd292-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="bd292-122">IOT Hub, milyonlarca eş zamanlı cihazı sağlar (bkz [kotalar ve azaltma][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="bd292-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="bd292-123">IOT hub'ı rasgele bölümleme izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="bd292-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="bd292-124">Cihaz bulut iletilerini bölümlenmiş kendi oluşturan bağlı **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="bd292-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="bd292-125">IOT Hub ve Event Hubs Hizmetleri arasındaki farklar hakkında daha fazla bilgi için bkz: [karşılaştırma Azure IOT Hub ve Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="bd292-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="bd292-126">Telemetri olmayan trafiği Gönder</span><span class="sxs-lookup"><span data-stu-id="bd292-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="bd292-127">Genellikle, telemetri veri noktaları ek olarak, iletileri ve ayrı yürütme ve çözüm arka ucu işlemede gerektiren isteklerinin aygıtları gönderin.</span><span class="sxs-lookup"><span data-stu-id="bd292-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="bd292-128">Arka uçtaki belirli bir eylemi tetikleyen gerekir Örneğin, kritik uyarılar.</span><span class="sxs-lookup"><span data-stu-id="bd292-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="bd292-129">Kolayca yazabilen bir [yönlendirme kuralı] [ lnk-devguide-custom] ya da bir başlığına bir ileti ya da bir değeri ileti gövdesi göre bunların işlenmesini adanmış bir uç nokta ileti türlerinden göndermek için.</span><span class="sxs-lookup"><span data-stu-id="bd292-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="bd292-130">Bu tür bir iletiyi işlemek için en iyi yolu hakkında daha fazla bilgi için bkz: [Öğreticisi: IOT Hub cihaz bulut iletilerini işlemek nasıl] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="bd292-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="bd292-131">Rota cihaz-bulut iletileri</span><span class="sxs-lookup"><span data-stu-id="bd292-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="bd292-132">Arka uç uygulamalarınızı cihaz-bulut iletileri yönlendirmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="bd292-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="bd292-133">Yerleşik kullanmak [Event Hub ile uyumlu uç nokta] [ lnk-compatible-endpoint] arka uç uygulamaların hub tarafından alınan cihaz bulut iletilerini okumanızı sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="bd292-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="bd292-134">Yerleşik Event Hub ile uyumlu uç noktası hakkında bilgi edinmek için [yerleşik uç noktasından cihaz bulut iletilerini okumanızı][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="bd292-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="bd292-135">IOT hub'ınızdaki özel uç noktaları iletileri göndermek için yönlendirme kurallarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd292-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="bd292-136">Olay hub'ları, Service Bus kuyruklarını veya Service Bus konu başlıklarını kullanarak cihaz bulut iletilerini okumanızı arka uç uygulamalarınızı özel uç noktaları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd292-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="bd292-137">Yönlendirme ve özel uç noktalar hakkında bilgi edinmek için [özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="bd292-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="bd292-138">Yanıltma özellikleri</span><span class="sxs-lookup"><span data-stu-id="bd292-138">Anti-spoofing properties</span></span>

<span data-ttu-id="bd292-139">Damgalar tüm cihaz IOT Hub, cihaz bulut iletilerini kimlik sahtekarlığı önlemek için aşağıdaki özelliklere sahip iletileri:</span><span class="sxs-lookup"><span data-stu-id="bd292-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="bd292-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="bd292-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="bd292-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="bd292-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="bd292-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="bd292-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="bd292-143">İlk iki içeren **DeviceID** ve **Generationıd** kaynak cihazın göre [aygıt kimlik özellikleri][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="bd292-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="bd292-144">**ConnectionAuthMethod** özelliği, aşağıdaki özelliklere sahip bir JSON serileştirilmiş nesne içerir:</span><span class="sxs-lookup"><span data-stu-id="bd292-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="bd292-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd292-145">Next steps</span></span>

<span data-ttu-id="bd292-146">Cihaz bulut iletilerini göndermek için kullanabileceğiniz SDK'ları hakkında bilgi için bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="bd292-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="bd292-147">[Get Started] [ lnk-get-started] öğreticileri sanal ve fiziksel aygıtlardan cihaz bulut iletilerini göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd292-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="bd292-148">Daha fazla ayrıntı için [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="bd292-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
