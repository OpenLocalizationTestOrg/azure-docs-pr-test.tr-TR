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
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>İleti yollarını ve özel uç noktaları için cihaz bulut iletilerini kullanın

IOT hub'ı etkinleştirir, tooroute [cihaz bulut iletilerini] [ lnk-device-to-cloud] tooIoT service'te Uç noktalara bağlı ileti özellikleri Hub. Esneklik toosend hello kuralları verin yönlendirme hello olmadan toogo gereken yeri iletileri ek hizmetler tooprocess iletileri veya toowrite ek kod gerekir. Yapılandırdığınız her yönlendirme kuralı hello aşağıdaki özelliklere sahiptir:

| Özellik      | Açıklama |
| ------------- | ----------- |
| **Ad**      | Merhaba kuralı tanımlayan hello benzersiz adı. |
| **Kaynak**    | Hello hello veri kaynağı üzerinde işlem toobe akış. Örneğin, cihaz telemetrisi. |
| **Koşul** | Merhaba ileti üstbilgilerini ve gövde karşı çalıştırmak ve hello uç noktası için bir eşleştirme olup olmadığını toodetermine kullanılan hello yönlendirme kuralı Hello sorgu ifadesi. Bir yol koşulu oluşturma hakkında daha fazla bilgi için bkz: Merhaba [başvuru - cihaz çiftlerini ve işleri için sorgu dili][lnk-devguide-query-language]. |
| **Uç noktası**  | Merhaba adı hello uç noktasının nereye IOT hub'ı hello koşuluyla eşleşen iletileri gönderir. Uç noktaları hello olmalıdır hello IOT hub'ı ile aynı bölgeye, aksi takdirde, ücret yansıtılmayacaktır çapraz bölge yazar için. |

Tek bir ileti durumda IOT hub'ı hello ileti toohello uç nokta her eşleşen kuralla ilişkili sunan birden çok yönlendirme kuralları hello koşula eşleşmiyor olabilir. IOT hub'ı tüm hello sahip birden çok ileti eşleşirse kuralları için ileti teslimi, aynı zamanda otomatik olarak deduplicates aynı hedefe yalnızca yazılmış toothat hedef kez.

IOT hub'ı varsayılan olan [yerleşik uç nokta][lnk-built-in]. Özel uç noktaları tooroute iletileri tooby abonelik toohello hub'ınızdaki diğer hizmetler bağlama oluşturabilirsiniz. IOT hub'ı şu anda özel uç noktalar olarak Event Hubs, Service Bus kuyrukları ve Service Bus konu başlıklarını destekler.

> [!WARNING]
> Service Bus kuyrukları ve konularından ile **oturumları** veya **yinelenen saptama** etkin özel uç noktalar olarak desteklenmez.

Özel uç noktaları IOT Hub oluşturma hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].

Özel uç noktaları okuma hakkında daha fazla bilgi için bkz:

* Okuma [olay hub'ları][lnk-getstarted-eh].
* Okuma [Service Bus kuyruklarını][lnk-getstarted-queue].
* Okuma [Service Bus konu başlıklarını][lnk-getstarted-topic].

### <a name="next-steps"></a>Sonraki adımlar

IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].

Merhaba sorgu dili hakkında daha fazla bilgi için toodefine yönlendirme kurallarını kullanın, bkz: [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili][lnk-devguide-query-language].

Merhaba [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] öğretici gösterir, size, nasıl toouse yönlendirme kuralları ve özel uç noktaları.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
