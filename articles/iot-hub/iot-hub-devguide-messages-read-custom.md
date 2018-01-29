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
ms.date: 11/29/2017
ms.author: dobett
ms.openlocfilehash: d1e22a4378caf69d2077d79f78682c4d438dbcd2
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/29/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>İleti yollarını ve özel uç noktaları için cihaz bulut iletilerini kullanın

IOT hub'ı etkinleştirir, yönlendirmek [cihaz bulut iletilerini] [ lnk-device-to-cloud] IOT Hub hizmeti dönük Uç noktalara ileti özelliklerine bağlı. Yönlendirme kuralları iletilerini işlemek için ek hizmetler gerek kalmadan Git veya ek kod yazmanız gereken yeri iletileri göndermek için esneklik sağlar. Yapılandırdığınız her yönlendirme kuralı aşağıdaki özelliklere sahiptir:

| Özellik      | Açıklama |
| ------------- | ----------- |
| **Ad**      | Kural tanımlayan benzersiz adı. |
| **Kaynak**    | Üzerinde işlem yapılması için veri akışı kaynağı. Örneğin, cihaz telemetrisi. |
| **Koşul** | İleti üstbilgilerini ve gövde karşı çalıştırmak ve uç nokta için bir eşleştirme olup olmadığını belirlemek için kullanılan yönlendirme kuralı için sorgu ifadesi. Yol koşulu oluşturma hakkında daha fazla bilgi için bkz: [başvuru - cihaz çiftlerini ve işleri için sorgu dili][lnk-devguide-query-language]. |
| **Uç noktası**  | Burada IOT hub'ı koşul eşleşen iletileri gönderir uç nokta adı. Uç noktaları, IOT hub'ı ile aynı bölgede olması gerekir, aksi takdirde, çapraz bölge yazma işlemleri için ücret. |

Tek bir ileti içinde durum IOT hub'ı iletiyi her eşleşen kuralla ilişkili uç teslim birden çok yönlendirme kuralları koşula eşleşmiyor olabilir. Tümü aynı hedefe sahip birden çok ileti eşleşirse kuralları için IOT hub'ı da otomatik olarak ileti teslimi, deduplicates, onu yalnızca bu hedefe kez yazılır.

IOT hub'ı varsayılan olan [yerleşik uç nokta][lnk-built-in]. Hub'ına diğer hizmetler aboneliğinizde bağlayarak iletileri yönlendirmek için özel uç noktaları oluşturabilirsiniz. IOT hub'ı şu anda Azure Storage kapsayıcıları, olay hub'ları, Service Bus kuyrukları ve Service Bus konu başlıklarını özel uç noktalar olarak destekler.

Yönlendirme ve özel uç noktaları kullandığınızda, tüm kurallar eşleşmiyorsa iletiler yalnızca yerleşik uç noktasına teslim edilir. Yerleşik uç da özel bir uç noktası için iletileri sunmak için iletileri gönderen yol eklemek **olayları** uç noktası.

> [!NOTE]
> IOT Hub, yalnızca Azure Storage kapsayıcıları bloblar için veri yazma destekler.

> [!WARNING]
> Service Bus kuyrukları ve konularından ile **oturumları** veya **yinelenen saptama** etkin özel uç noktalar olarak desteklenmez.

Özel uç noktaları IOT Hub oluşturma hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].

Özel uç noktaları okuma hakkında daha fazla bilgi için bkz:

* Okuma [Azure Storage kapsayıcıları][lnk-getstarted-storage].
* Okuma [olay hub'ları][lnk-getstarted-eh].
* Okuma [Service Bus kuyruklarını][lnk-getstarted-queue].
* Okuma [Service Bus konu başlıklarını][lnk-getstarted-topic].

### <a name="next-steps"></a>Sonraki adımlar

IOT Hub uç noktaları hakkında daha fazla bilgi için bkz: [IOT Hub uç noktaları][lnk-devguide-endpoints].

Yönlendirme kurallarını tanımlamak için kullandığınız sorgu dili hakkında daha fazla bilgi için bkz: [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili][lnk-devguide-query-language].

[Yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] öğretici yönlendirme kuralları ve özel uç noktaları nasıl kullanılacağını gösterir.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
[lnk-getstarted-storage]: ../storage/blobs/storage-blobs-introduction.md
