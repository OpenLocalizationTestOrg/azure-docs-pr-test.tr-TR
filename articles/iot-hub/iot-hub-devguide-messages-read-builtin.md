---
title: "aaaUnderstand hello Azure IOT hub'ı yerleşik uç | Microsoft Docs"
description: "Geliştirici Kılavuzu - nasıl toouse hello yerleşik, Event Hub ile uyumlu uç noktası o cihaz bulut iletilerini açıklar."
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="11a46-103">Merhaba yerleşik uç noktasından cihaz bulut iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="11a46-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="11a46-104">Varsayılan olarak, iletileri yönlendirilmiş toohello yerleşik service'e yönelik uç noktası olan (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="11a46-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="11a46-105">Bu uç noktası şu anda olup yalnızca hello kullanılarak kullanıma sunulan [AMQP] [ lnk-amqp] bağlantı noktası 5671 protokolü.</span><span class="sxs-lookup"><span data-stu-id="11a46-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="11a46-106">IOT hub'ı hello sunan özellikleri tooenable, toocontrol hello yerleşik Event Hub ile uyumlu Mesajlaşma uç nokta **iletileri/olayları**.</span><span class="sxs-lookup"><span data-stu-id="11a46-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="11a46-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="11a46-107">Property</span></span>            | <span data-ttu-id="11a46-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="11a46-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="11a46-109">**Bölüm sayısı**</span><span class="sxs-lookup"><span data-stu-id="11a46-109">**Partition count**</span></span> | <span data-ttu-id="11a46-110">Bu özellik oluşturma toodefine hello kümesi sayısı [bölümleri] [ lnk-event-hub-partitions] cihaz-bulut olay alımı için.</span><span class="sxs-lookup"><span data-stu-id="11a46-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="11a46-111">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="11a46-111">**Retention time**</span></span>  | <span data-ttu-id="11a46-112">Bu özellik ne kadar süreyle iletileri IOT Hub tarafından korunur gün cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="11a46-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="11a46-113">Merhaba varsayılan bir günüdür ancak artan tooseven gün olabilir.</span><span class="sxs-lookup"><span data-stu-id="11a46-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="11a46-114">IOT Hub ayrıca sağlar toomanage tüketici grupları hello yerleşik cihaz-bulut uç noktası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="11a46-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="11a46-115">Varsayılan olarak, açıkça bir ileti yönlendirme kuralı ile eşleşmiyor tüm iletileri toohello yerleşik endpoint yazılır.</span><span class="sxs-lookup"><span data-stu-id="11a46-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="11a46-116">Bu geri dönüş yolu devre dışı bırakırsanız, tüm ileti yönlendirme kuralları açıkça eşleşmiyor iletileri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="11a46-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="11a46-117">Merhaba bekletme süresini, hello yoluyla programlı olarak değiştirmek [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis], veya hello kullanarak [Azure portal] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="11a46-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="11a46-118">IOT hub'ı sunan hello **iletileri/olayları** yerleşik uç noktası arka ucunuz için hub tarafından alınan tooread hello cihaz bulut iletilerini Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="11a46-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="11a46-119">Bu uç noktaya olaydır hello mekanizmaları hello Event Hubs hizmetinin destekler iletileri okumak için toouse sağlayan Hub ile uyumlu.</span><span class="sxs-lookup"><span data-stu-id="11a46-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="11a46-120">Merhaba yerleşik uç noktasından okumak</span><span class="sxs-lookup"><span data-stu-id="11a46-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="11a46-121">Merhaba kullandığınızda [.NET için Azure hizmet veri yolu SDK] [ lnk-servicebus-sdk] veya hello [Event Hubs - olay işleyicisi konağı][lnk-eventprocessorhost], herhangi bir IOT Hub bağlantısı kullanabilirsiniz dizeleri hello doğru izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="11a46-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="11a46-122">Ardından **iletileri/olayları** hello olay hub'ı adı olarak.</span><span class="sxs-lookup"><span data-stu-id="11a46-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="11a46-123">SDK'ları (veya ürün tümleştirmeler) kullandığınızda, IOT hub'ını farkında, hello IOT hub'ı ayarlarından hello bir Event Hub ile uyumlu uç noktası ve Event Hub ile uyumlu adı almalısınız [Azure portal] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="11a46-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="11a46-124">Merhaba IOT hub dikey penceresinde tıklayın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="11a46-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="11a46-125">Merhaba, **yerleşik uç noktaları** 'yi tıklatın **olayları**.</span><span class="sxs-lookup"><span data-stu-id="11a46-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="11a46-126">Merhaba dikey içeren değerleri aşağıdaki hello: **Event Hub ile uyumlu uç nokta**, **Event Hub ile uyumlu adı**, **bölümleri**, **bekletme süresini**, ve **tüketici grupları**.</span><span class="sxs-lookup"><span data-stu-id="11a46-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Cihaz bulut ayarları][img-eventhubcompatible]

<span data-ttu-id="11a46-128">Merhaba IOT Hub SDK'sı gerektirir hello olan IOT Hub uç nokta adı **iletileri/olayları** hello gösterildiği gibi **uç noktaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="11a46-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="11a46-129">Merhaba kullanmakta olduğunuz SDK gerektiriyorsa bir **ana bilgisayar adı** veya **Namespace** değeri, hello hello düzenini kaldırmak **Event Hub ile uyumlu uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="11a46-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="11a46-130">Örneğin, Event Hub ile uyumlu uç noktanızı ise **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **ana bilgisayar adı** olacaktır ** iothub-ns-myiothub-1234.servicebus.windows.net**ve hello **Namespace** olacaktır **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="11a46-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="11a46-131">Merhaba sahip herhangi bir paylaşılan erişim ilkesinin sonra kullanabileceğiniz **ServiceConnect** izinleri tooconnect toohello belirtilen olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="11a46-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="11a46-132">Merhaba önceki bilgileri kullanarak bir Event Hub bağlantı dizesi toobuild ihtiyacınız varsa, desen aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="11a46-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="11a46-133">Merhaba SDK'ları ve IOT hub'ı gösteren Event Hub ile uyumlu uç noktalar ile kullanabileceğiniz tümleştirmeler listesi aşağıdaki hello hello öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="11a46-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="11a46-134">[Java Event Hubs istemcisi](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="11a46-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="11a46-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="11a46-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="11a46-136">Merhaba görüntüleyebilirsiniz [kaynak spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) github'da.</span><span class="sxs-lookup"><span data-stu-id="11a46-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="11a46-137">[Apache Spark tümleştirme](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="11a46-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11a46-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11a46-138">Next steps</span></span>

<span data-ttu-id="11a46-139">IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="11a46-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="11a46-140">Merhaba [Get Started] [ lnk-get-started] öğreticileri, nasıl toosend cihaz bulut iletilerini benzetimli aygıtları ve Göster Merhaba iletileri hello yerleşik uç noktasından okumak.</span><span class="sxs-lookup"><span data-stu-id="11a46-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="11a46-141">Merhaba daha ayrıntılı bilgi için bkz: [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="11a46-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="11a46-142">Tooroute istiyorsanız toocustom uç noktaları, cihaz-bulut iletileri için bkz: [için cihaz bulut iletilerini ileti yollarını ve özel uç noktaları kullanma][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="11a46-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
