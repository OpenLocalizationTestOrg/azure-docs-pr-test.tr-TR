---
title: "aaaCompare Azure IOT Hub tooAzure olay hub'ları | Microsoft Docs"
description: "Merhaba IOT Hub ve olay hub'ları Azure Hizmetleri işlevsel farklılıklar ve kullanım örnekleri vurgulama karşılaştırması. Desteklenen protokoller, cihaz yönetimi, izleme, Hello karşılaştırma içerir ve dosyayı yükler."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Azure IOT Hub ve Azure Event Hubs karşılaştırması
IOT hub'ına yönelik hello ana kullanım örnekleri toogather telemetri aygıtlardan biri. Bu nedenle, IOT hub'ı genellikle çok karşılaştırılır[Azure Event Hubs][Azure Event Hubs]. IOT Hub gibi olay hub'ları telemetri girişi sağlayan hizmetini işleme bir olaydır düşük gecikme süreli ve yüksek güvenilirlikle büyük ölçekte toohello bulut.

Ancak, hello Hizmetleri aşağıdaki tablonun hello ayrıntılı birçok farklar vardır:

| Alan | IoT Hub’ı | Event Hubs |
| --- | --- | --- |
| Kimlik doğrulaması desenleri | Etkinleştirir [cihaz bulut iletişimleri] [ lnk-d2c-guidance] (yüklemeleri ve bildirilen özellikleri Mesajlaşma, dosya) ve [bulut-cihaz iletişimi] [ lnk-c2d-guidance] (doğrudan yöntemleri, Mesajlaşma istenen özellikleri). |Yalnızca olay giriş (genellikle cihaz bulut senaryoları için kabul) sağlar. |
| Cihaz durumu bilgileri | [Cihaz çiftlerini] [ lnk-twins] depolayabilir ve sorgu aygıt durum bilgileri. | Aygıt durum bilgisi depolanabilir. |
| Cihaz protokol desteği |MQTT, MQTT WebSockets, AMQP, WebSockets ve HTTP üzerinden AMQP üzerinden destekler. Ayrıca, IOT Hub ile Merhaba çalışır [Azure IOT protokolü ağ geçidini][lnk-azure-protocol-gateway], bir özelleştirilebilir protokol ağ geçidi uygulaması toosupport özel protokoller. |AMQP, AMQP WebSockets ve HTTP üzerinden destekler. |
| Güvenlik |Cihaz başına kimlik ve iptal edilebilir erişim denetimi sağlar. Merhaba bkz [hello IOT Hub Geliştirici Kılavuzu'nun güvenlik bölümüne]. |Olay hub'ları genelinde sağlar [paylaşılan erişim ilkeleri][Event Hubs - security], ile sınırlı iptalini desteklemek aracılığıyla [publisher'ın ilkeleri][Event Hubs publisher policies]. IOT çözümleri çoğunlukla gerekli tooimplement bir özel çözüm toosupport cihaz başına kimlik bilgilerini ve ölçüleri yanıltma olur. |
| İşlemleri izleme |IOT çözümleri toosubscribe tooa zengin bir cihaz kimlik doğrulama hataları, azaltma ve hatalı biçim özel durumlar gibi cihaz kimlik yönetimi ve bağlantı olayları sağlar. Bu olaylar etkinleştirmeniz tooquickly hello tek tek cihaz düzeyinde bağlantı sorunlarını tanımlayın. |Yalnızca toplama ölçümleri kullanıma sunar. |
| Ölçek |En iyi duruma getirilmiş toosupport milyonlarca eş zamanlı cihazı olur. |Metre hello olarak başına bağlantı [Azure Event Hubs kotaları][Azure Event Hubs quotas]. Üzerindeki diğer yandan Merhaba, olay hub'ları toospecify hello bölüm gönderilen her ileti için etkinleştirir. |
| Cihaz SDK'ları |Sağlar [cihaz SDK'ları] [ Azure IoT SDKs] büyük çeşitli platformlar ve diller, toplama toodirect MQTT, AMQP ve HTTP API'leri için. |.NET, Java ve C toplama tooAMQP ve HTTP gönderme arabirimleri desteklenir. |
| Karşıya dosya yükleme |IOT çözümleri tooupload aygıtları toohello bulut dosyalarından sağlar. İş akışı tümleştirme ve hata ayıklama desteği için kategori izleme işlemleri için bir dosya bildirim uç noktası içerir. | Desteklenmiyor. |
| Rota toomultiple uç noktaları iletileri | Too10 özel uç noktaları desteklenir. Kurallar, iletileri yönlendirilmiş toocustom uç noktaları şeklini belirler. Daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging]. | Yazılan ve ileti gönderme için barındırılan ek kod toobe gerektirir. |

Merhaba yalnızca kullanım örneği cihaz bulut telemetri giriş olsa bile Özet olarak, IOT hub'ı IOT cihaz bağlantısı için tasarlanmış bir hizmet sağlar. Bu senaryolarında IOT özgü özelliklerle tooexpand hello değer önermeleri devam eder. Olay hub'ları bir büyük ölçekte, hem de ağlar arası veri merkezi ve içi veri merkezi senaryoları Merhaba içeriğine olay giriş için tasarlanmıştır.

Seyrek toouse değil IOT Hub ve Event Hubs hello aynı çözümü. Olay hub'ları aşama sonraki olay giriş gerçek zamanlı işleme altyapısı işler ve IOT hub'ı hello cihaz bulut iletişimi işler.

### <a name="next-steps"></a>Sonraki adımlar
IOT hub'ı dağıtımınızı planlama hakkında daha fazla toolearn bkz [ölçeklendirme, HA ve DR][lnk-scaling].

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[hello IOT Hub Geliştirici Kılavuzu'nun güvenlik bölümüne]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
