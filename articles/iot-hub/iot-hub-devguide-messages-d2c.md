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
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Cihaz bulut iletilerini tooIoT Hub Gönder

toosend zaman serisi telemetri ve aygıtları tooyour çözüm arka ucunuz, uyarılar, aygıt tooyour IOT hub'dan cihaz bulut iletilerini gönderir. IOT Hub tarafından desteklenen diğer cihaz bulut seçenekleri tartışma için bkz [cihaz bulut iletişimleri Kılavuzu][lnk-d2c-guidance].

Bir aygıt'e yönelik uç noktası aracılığıyla cihaz bulut iletilerini gönder (**/devices/ {DeviceID} / iletileri/olayları**). Yönlendirme kuralları ardından, IOT hub'ına, iletileri tooone hello service'e yönelik uç noktalar için rota. Yönlendirme kuralları kullanmak hello üstbilgiler ve, hub toodetermine akan hello cihaz bulut iletilerini gövdesi nerede tooroute bunları. Varsayılan olarak, iletileri yönlendirilmiş toohello yerleşik service'e yönelik uç noktası olan (**iletileri/olayları**), diğer bir deyişle uyumlu [Event Hubs][lnk-event-hubs]. Bu nedenle, standart kullanabilirsiniz [olay hub'ları tümleştirme ve SDK] [ lnk-compatible-endpoint] tooreceive cihaz bulut iletilerini çözümünüzdeki son yedekleme.

IOT Hub cihaz bulut akış Mesajlaşma düzeni kullanarak ileti uygular. IOT Hub'ın cihaz bulut iletilerini gibi daha fazla [Event Hubs] [ lnk-event-hubs] *olayları* daha [Service Bus] [ lnk-servicebus] *iletileri* birden çok okuyucular tarafından okunabilir hello hizmeti aracılığıyla geçirme olayları hacmi yüksek olmasını durumunda.

Cihaz bulut IOT Hub ile Mesajlaşma hello aşağıdaki özelliklere sahiptir:

* Cihaz bulut iletilerini sağlam ve bir IOT hub'ın varsayılan saklama **iletileri/olayları** tooseven günlerini uç noktası için.
* Cihaz bulut iletilerini en fazla 256 KB olabilir ve toooptimize gönderir toplu olarak gruplandırılabilir. Toplu işlemler en fazla 256 KB olabilir.
* Hello açıklandığı gibi [Denetim erişim tooIoT Hub] [ lnk-devguide-security] bölüm, IOT Hub cihaz başına kimlik doğrulama ve erişim denetimi sağlar.
* IOT hub'ı too10 özel uç noktaları yukarı toocreate sağlar. İletiler toohello uç noktaları, IOT hub'ına yapılandırılmış yolları göre teslim edilir. Daha fazla bilgi için bkz: [yönlendirme kuralları](#routing-rules).
* IOT Hub, milyonlarca eş zamanlı cihazı sağlar (bkz [kotalar ve azaltma][lnk-quotas]).
* IOT hub'ı rasgele bölümleme izin vermiyor. Cihaz bulut iletilerini bölümlenmiş kendi oluşturan bağlı **DeviceID**.

Merhaba hello IOT Hub ve Event Hubs Hizmetleri arasındaki farklar hakkında daha fazla bilgi için bkz: [karşılaştırma Azure IOT Hub ve Azure Event Hubs][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Telemetri olmayan trafiği Gönder

Genellikle, ayrıca tootelemetry veri noktaları, aygıtlar iletileri ayrı yürütme ve hello çözüm arka ucu işlemede gerektiren istekleri göndermek ve. Örneğin, hello içinde belirli bir eylemi tetikleyen gereken kritik uyarılar arka uç. Kolayca yazabilen bir [yönlendirme kuralı] [ lnk-devguide-custom] toosend iletileri tooan uç noktası bu tür adanmış bir ya da başlığında selamlama iletisine ya da hello ileti gövdesi bir değere göre tootheir işleme.

Merhaba hello en iyi şekilde tooprocess ileti bu tür hakkında daha fazla bilgi için bkz: [Öğreticisi: nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.

## <a name="route-device-to-cloud-messages"></a>Rota cihaz-bulut iletileri

Yönlendirme cihaz bulut iletilerini tooyour arka uç uygulamalar için iki seçeneğiniz vardır:

* Merhaba yerleşik kullanmak [Event Hub ile uyumlu uç nokta] [ lnk-compatible-endpoint] tooenable arka uç uygulamaları tooread hello cihaz bulut iletilerini hello hub tarafından alınan. toolearn hello yerleşik Event Hub ile uyumlu uç noktasını hakkında bkz [hello yerleşik uç noktasından cihaz bulut iletilerini okumanızı][lnk-devguide-builtin].
* Yönlendirme kuralları toosend iletileri toocustom uç noktaları IOT hub'ınızı kullanın. Olay hub'ları, Service Bus kuyruklarını veya Service Bus konu başlıklarını kullanma, arka uç uygulamaları tooread cihaz bulut iletilerini özel uç noktaları etkinleştirin. Yönlendirme ve özel uç noktaları hakkında toolearn bkz [özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Yanıltma özellikleri

IOT Hub, cihaz bulut iletilerini hello aşağıdaki özelliklere tüm iletileri Damgalar yanıltma tooavoid aygıt:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Merhaba ilk iki hello içeren **DeviceID** ve **Generationıd** göre aygıtı kaynaklanan Merhaba, [aygıt kimlik özellikleri][lnk-device-properties].

Merhaba **ConnectionAuthMethod** özelliği hello aşağıdaki özelliklere bir JSON serileştirilmiş nesne içerir:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba SDK'ları hakkında bilgi için toosend cihaz bulut iletilerini kullanın, bkz: [Azure IOT SDK'ları][lnk-sdks].

Merhaba [Get Started] [ lnk-get-started] öğreticiler gösterir, sanal ve fiziksel aygıtlardan nasıl toosend cihaz-bulut iletileri. Merhaba daha ayrıntılı bilgi için bkz: [yolları kullanma işlemi IOT Hub cihaz bulut iletilerini] [ lnk-d2c-tutorial] Öğreticisi.

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
