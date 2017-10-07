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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Merhaba yerleşik uç noktasından cihaz bulut iletilerini okuyun

Varsayılan olarak, iletileri yönlendirilmiş toohello yerleşik service'e yönelik uç noktası olan (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs]. Bu uç noktası şu anda olup yalnızca hello kullanılarak kullanıma sunulan [AMQP] [ lnk-amqp] bağlantı noktası 5671 protokolü. IOT hub'ı hello sunan özellikleri tooenable, toocontrol hello yerleşik Event Hub ile uyumlu Mesajlaşma uç nokta **iletileri/olayları**.

| Özellik            | Açıklama |
| ------------------- | ----------- |
| **Bölüm sayısı** | Bu özellik oluşturma toodefine hello kümesi sayısı [bölümleri] [ lnk-event-hub-partitions] cihaz-bulut olay alımı için. |
| **Saklama süresi**  | Bu özellik ne kadar süreyle iletileri IOT Hub tarafından korunur gün cinsinden belirtir. Merhaba varsayılan bir günüdür ancak artan tooseven gün olabilir. |

IOT Hub ayrıca sağlar toomanage tüketici grupları hello yerleşik cihaz-bulut uç noktası alırsınız.

Varsayılan olarak, açıkça bir ileti yönlendirme kuralı ile eşleşmiyor tüm iletileri toohello yerleşik endpoint yazılır. Bu geri dönüş yolu devre dışı bırakırsanız, tüm ileti yönlendirme kuralları açıkça eşleşmiyor iletileri bırakılır.

Merhaba bekletme süresini, hello yoluyla programlı olarak değiştirmek [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis], veya hello kullanarak [Azure portal] [ lnk-management-portal].

IOT hub'ı sunan hello **iletileri/olayları** yerleşik uç noktası arka ucunuz için hub tarafından alınan tooread hello cihaz bulut iletilerini Hizmetleri. Bu uç noktaya olaydır hello mekanizmaları hello Event Hubs hizmetinin destekler iletileri okumak için toouse sağlayan Hub ile uyumlu.

## <a name="read-from-hello-built-in-endpoint"></a>Merhaba yerleşik uç noktasından okumak

Merhaba kullandığınızda [.NET için Azure hizmet veri yolu SDK] [ lnk-servicebus-sdk] veya hello [Event Hubs - olay işleyicisi konağı][lnk-eventprocessorhost], herhangi bir IOT Hub bağlantısı kullanabilirsiniz dizeleri hello doğru izinlere sahip. Ardından **iletileri/olayları** hello olay hub'ı adı olarak.

SDK'ları (veya ürün tümleştirmeler) kullandığınızda, IOT hub'ını farkında, hello IOT hub'ı ayarlarından hello bir Event Hub ile uyumlu uç noktası ve Event Hub ile uyumlu adı almalısınız [Azure portal] [ lnk-management-portal]:

1. Merhaba IOT hub dikey penceresinde tıklayın **uç noktaları**.
1. Merhaba, **yerleşik uç noktaları** 'yi tıklatın **olayları**. Merhaba dikey içeren değerleri aşağıdaki hello: **Event Hub ile uyumlu uç nokta**, **Event Hub ile uyumlu adı**, **bölümleri**, **bekletme süresini**, ve **tüketici grupları**.

    ![Cihaz bulut ayarları][img-eventhubcompatible]

Merhaba IOT Hub SDK'sı gerektirir hello olan IOT Hub uç nokta adı **iletileri/olayları** hello gösterildiği gibi **uç noktaları** dikey.

Merhaba kullanmakta olduğunuz SDK gerektiriyorsa bir **ana bilgisayar adı** veya **Namespace** değeri, hello hello düzenini kaldırmak **Event Hub ile uyumlu uç nokta**. Örneğin, Event Hub ile uyumlu uç noktanızı ise **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **ana bilgisayar adı** olacaktır ** iothub-ns-myiothub-1234.servicebus.windows.net**ve hello **Namespace** olacaktır **iothub-ns-myiothub-1234**.

Merhaba sahip herhangi bir paylaşılan erişim ilkesinin sonra kullanabileceğiniz **ServiceConnect** izinleri tooconnect toohello belirtilen olay hub'ı.

Merhaba önceki bilgileri kullanarak bir Event Hub bağlantı dizesi toobuild ihtiyacınız varsa, desen aşağıdaki hello kullanın:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Merhaba SDK'ları ve IOT hub'ı gösteren Event Hub ile uyumlu uç noktalar ile kullanabileceğiniz tümleştirmeler listesi aşağıdaki hello hello öğeleri içerir:

* [Java Event Hubs istemcisi](https://github.com/hdinsight/eventhubs-client).
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Merhaba görüntüleyebilirsiniz [kaynak spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) github'da.
* [Apache Spark tümleştirme](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Sonraki adımlar

IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-endpoints].

Merhaba [Get Started] [ lnk-get-started] öğreticileri, nasıl toosend cihaz bulut iletilerini benzetimli aygıtları ve Göster Merhaba iletileri hello yerleşik uç noktasından okumak. Merhaba daha ayrıntılı bilgi için bkz: [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.

Tooroute istiyorsanız toocustom uç noktaları, cihaz-bulut iletileri için bkz: [için cihaz bulut iletilerini ileti yollarını ve özel uç noktaları kullanma][lnk-custom].

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
