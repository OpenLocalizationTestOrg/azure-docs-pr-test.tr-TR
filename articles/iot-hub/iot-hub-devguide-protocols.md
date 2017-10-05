---
title: "Azure IOT hub'ı iletişim protokolleri ve bağlantı noktaları | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihaz Bulut ve bulut-cihaz iletişimi ve açık bağlantı noktası numaraları için desteklenen iletişim protokolleri açıklar."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 98004a48734e33f85eebf8f6213d9f0751dea843
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# Başvuru - iletişim protokolü seçin

IOT hub'ı cihazların kullanmasına izin verir [MQTT][lnk-mqtt], MQTT WebSockets, üzerinden [AMQP][lnk-amqp], AMQP WebSockets ve HTTP üzerinden iletişim kuralları için cihaz tarafı iletişim. Bu protokollerin belirli IOT Hub özellikleri nasıl desteği hakkında daha fazla bilgi için bkz: [cihaz bulut iletişimleri Kılavuzu] [ lnk-d2c-guidance] ve [bulut-cihaz iletişimi Kılavuzu] [lnk-c2d-guidance].

Aşağıdaki tabloda, tercih ettiğiniz Protokolü yönelik üst düzey öneriler sağlar:

| Protokol | Bu protokol seçtiğinizde |
| --- | --- |
| MQTT <br> WebSocket üzerinden MQTT |Birden çok aygıt (her kendi cihaz başına kimlik bilgileriyle) aynı TLS bağlantısı üzerinden bağlanmak için gerekli değil tüm cihazlarda kullanın. |
| AMQP <br> AMQP WebSocket üzerinden |Aygıtlarda çoğullama bağlantı yararlanmak için alan ve bulut ağ geçidi kullanın. |
| HTTP |Diğer protokolleri destekleyemez cihazlar için kullanın. |

Cihaz tarafındaki iletişimleri için protokol seçtiğinizde aşağıdaki noktaları göz önünde bulundurun:

* **Bulut cihaz düzeni**. HTTP sunucusu itme uygulamak için etkili bir yol yok. Bu nedenle, HTTP kullanırken, cihazlar IOT Hub için bulut-cihaz iletilerini yoklar. Bu yaklaşım aygıt ve IOT Hub için yetersiz olduğunu. Geçerli HTTP yönergeleri altında her aygıt için iletileri 25 dakikada bir veya daha fazla yoklama. Diğer taraftan, MQTT ve AMQP, bulut-cihaz iletilerini alırken sunucu itme destekler. Bunlar, anında bildirim iletilerinin IOT hub'dan cihaz için etkinleştirin. Teslim gecikme ilgili bir sorun varsa, MQTT veya AMQP kullanmak için en iyi protokolleri edilir. Nadiren bağlanan cihazlar için HTTP de çalışır.
* **Alan ağ geçitleri**. MQTT ve HTTP kullanırken, birden çok aygıt (her kendi cihaz başına kimlik bilgileriyle) bağlanamıyor aynı TLS bağlantısı kullanarak. Bu nedenle, için [alan ağ geçidi senaryoları][lnk-azure-gateway-guidance], her cihaz için alan ağ geçidi ve IOT hub'ı arasında TLS bağlantı bağlı alan ağ geçidi için bir gerektirdiğinden bu protokollerin yetersiz.
* **Düşük kaynak aygıtları**. MQTT ve HTTP kitaplıkları AMQP kitaplıkları daha küçük bir yer vardır. Cihaz kaynakları (örneğin'den az 1 MB RAM) sınırlıdır, bu nedenle, bu protokollere yalnızca protokol uygulanması olabilir.
* **Ağ geçişi**. Bağlantı noktasındaki HTTP olmayan protokolleri kapalı ağlarında sorunlara neden olabilecek 8883, MQTT dinler sırada bağlantı noktası 5671, standart AMQP protokolünü kullanır. MQTT WebSockets üzerinden AMQP WebSockets ve HTTP üzerinden bu senaryoda amacıyla kullanılabilir.
* **Yükü boyutu**. MQTT ve AMQP HTTP değerinden daha küçük yüklerini sonucunda ikili protokoller şunlardır.

> [!WARNING]
> HTTP kullanırken, her cihaz için bulut-cihaz iletilerini 25 dakikada bir veya daha fazla yoklama. Ancak, geliştirme sırasında 25 dakikada daha sık yoklamak için kabul edilebilir.

## Bağlantı noktası numaraları

Aygıtları çeşitli protokoller kullanarak Azure IOT Hub ile iletişim kurabilir. Genellikle, Protokol seçimi çözümü belirli gereksinimleri tarafından yönetilir. Aşağıdaki tabloda, belirli bir iletişim kuralı kullanabilmek bir cihaz için açık olmalıdır giden bağlantı noktalarını listeler:

| Protokol | Bağlantı noktası |
| --- | --- |
| MQTT |8883 |
| WebSockets üzerinden MQTT |443 |
| AMQP |5671 |
| AMQP WebSockets üzerinden |443 |
| HTTP |443 |

Bir Azure bölgesinde bir IOT hub'ı oluşturduğunuzda, IOT hub'ı bu IOT hub'ın ömrü boyunca aynı IP adresini tutar. Ancak, Microsoft farklı ölçek birimi için IOT hub'ı taşınırsa hizmet kalitesi korumak için daha sonra yeni bir IP adresi atanır.


## Sonraki adımlar

IOT hub'ı MQTT Protokolü nasıl uyguladığını hakkında daha fazla bilgi için bkz: [MQTT protokolünü kullanarak, IOT hub ile iletişim kurun][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
