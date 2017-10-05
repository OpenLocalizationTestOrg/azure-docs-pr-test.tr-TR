---
title: "Azure IOT hub'ı yerleşik uç anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - yerleşik, Event Hub ile uyumlu uç noktası o cihaz bulut iletilerini kullanmayı açıklar."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="7da0b-103">Yerleşik uç noktasından cihaz bulut iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="7da0b-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="7da0b-104">Varsayılan olarak, yerleşik service'e yönelik uç noktasına iletileri yönlendirilir (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="7da0b-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="7da0b-105">Bu bitiş noktası şu anda yalnızca gösterilen kullanmaktır [AMQP] [ lnk-amqp] bağlantı noktası 5671 protokolü.</span><span class="sxs-lookup"><span data-stu-id="7da0b-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="7da0b-106">IOT hub'ı yerleşik Event Hub ile uyumlu Mesajlaşma uç nokta denetlemenize olanak sağlamak için aşağıdaki özellikleri sunar **iletileri/olayları**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="7da0b-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="7da0b-107">Property</span></span>            | <span data-ttu-id="7da0b-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7da0b-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="7da0b-109">**Bölüm sayısı**</span><span class="sxs-lookup"><span data-stu-id="7da0b-109">**Partition count**</span></span> | <span data-ttu-id="7da0b-110">Oluşturma sırasında sayısını tanımlamak için bu özelliği ayarlamak [bölümleri] [ lnk-event-hub-partitions] cihaz-bulut olay alımı için.</span><span class="sxs-lookup"><span data-stu-id="7da0b-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="7da0b-111">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="7da0b-111">**Retention time**</span></span>  | <span data-ttu-id="7da0b-112">Bu özellik ne kadar süreyle iletileri IOT Hub tarafından korunur gün cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="7da0b-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="7da0b-113">Varsayılan bir gündür, ancak yedi gün sayısı artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7da0b-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="7da0b-114">IOT Hub ayrıca yönetmenize imkan sağlar tüketici grupları yerleşik cihaz-bulut uç noktası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7da0b-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="7da0b-115">Varsayılan olarak, açıkça bir ileti yönlendirme kuralı ile eşleşmiyor tüm iletileri yerleşik uç noktasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7da0b-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="7da0b-116">Bu geri dönüş yolu devre dışı bırakırsanız, tüm ileti yönlendirme kuralları açıkça eşleşmiyor iletileri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7da0b-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="7da0b-117">Bekletme süresini ya da değiştirebilirsiniz üzerinden programlı olarak [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis], veya kullanarak [Azure portal][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="7da0b-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="7da0b-118">IOT hub'ı sunan **iletileri/olayları** hub tarafından alınan cihaz bulut iletilerini okumanızı arka uç hizmetleriniz için yerleşik bir uç nokta.</span><span class="sxs-lookup"><span data-stu-id="7da0b-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="7da0b-119">Bu uç noktaya olaydır iletileri okumak için Event Hubs hizmeti mekanizmaları birini kullanmanızı sağlayan Hub ile uyumlu destekler.</span><span class="sxs-lookup"><span data-stu-id="7da0b-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="7da0b-120">Yerleşik uç noktasından okumak</span><span class="sxs-lookup"><span data-stu-id="7da0b-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="7da0b-121">Kullandığınızda [.NET için Azure hizmet veri yolu SDK] [ lnk-servicebus-sdk] veya [Event Hubs - olay işleyicisi konağı][lnk-eventprocessorhost], doğru izinlere sahip IOT Hub bağlantı dizelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da0b-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="7da0b-122">Ardından **iletileri/olayları** olay hub'ı adı olarak.</span><span class="sxs-lookup"><span data-stu-id="7da0b-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="7da0b-123">SDK'ları (veya ürün tümleştirmeler) kullandığınızda, IOT hub'ını farkında, IOT hub'ı ayarlarından bir Event Hub ile uyumlu uç noktası ve Event Hub ile uyumlu adı almalısınız [Azure portal][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="7da0b-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="7da0b-124">IOT hub dikey penceresinde tıklayın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="7da0b-125">İçinde **yerleşik uç noktaları** 'yi tıklatın **olayları**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="7da0b-126">Dikey penceresinde şu değerleri içeriyor: **Event Hub ile uyumlu uç nokta**, **Event Hub ile uyumlu adı**, **bölümleri**, **bekletme süresini**, ve **tüketici grupları**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Cihaz bulut ayarları][img-eventhubcompatible]

<span data-ttu-id="7da0b-128">IOT Hub SDK'sı olan IOT Hub uç nokta adı gerektirir **iletileri/olayları** gösterildiği gibi **uç noktaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="7da0b-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="7da0b-129">Kullanmakta olduğunuz SDK gerektiriyorsa bir **ana bilgisayar adı** veya **Namespace** değeri, düzeninden Kaldır **Event Hub ile uyumlu uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="7da0b-130">Örneğin, Event Hub ile uyumlu uç noktanızı ise **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, **ana bilgisayar adı** olacaktır **iothub-ns-myiothub-1234.servicebus.windows.net**ve **Namespace** olacaktır **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="7da0b-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="7da0b-131">Daha sonra sahip herhangi bir paylaşılan erişim ilkesinin kullanabilirsiniz **ServiceConnect** belirtilen olay Hub'ına bağlanmak için gereken izinleri.</span><span class="sxs-lookup"><span data-stu-id="7da0b-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="7da0b-132">Önceki bilgileri kullanarak bir Event Hub bağlantı dizesi oluşturma gerekiyorsa, şu biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="7da0b-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="7da0b-133">SDK'ları ve IOT hub'ı gösteren Event Hub ile uyumlu uç noktalar ile kullanabileceğiniz tümleştirmeler, aşağıdaki listedeki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="7da0b-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="7da0b-134">[Java Event Hubs istemcisi](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="7da0b-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="7da0b-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7da0b-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="7da0b-136">Görüntüleyebileceğiniz [kaynak spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) github'da.</span><span class="sxs-lookup"><span data-stu-id="7da0b-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="7da0b-137">[Apache Spark tümleştirme](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="7da0b-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7da0b-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7da0b-138">Next steps</span></span>

<span data-ttu-id="7da0b-139">IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="7da0b-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="7da0b-140">[Get Started] [ lnk-get-started] öğreticileri benzetimli aygıtlardan cihaz bulut iletilerini göndermek ve iletileri yerleşik uç noktasından okumak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="7da0b-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="7da0b-141">Daha fazla ayrıntı için [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7da0b-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="7da0b-142">Özel uç noktaları için cihaz bulut iletilerini yönlendirmek istiyorsanız, bkz: [için cihaz bulut iletilerini ileti yollarını ve özel uç noktaları kullanma][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="7da0b-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
