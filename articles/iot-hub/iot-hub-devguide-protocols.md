---
title: "aaaAzure IOT hub'ı iletişimi protokoller ve bağlantı noktaları | Microsoft Docs"
description: "Geliştirici Kılavuzu - desteklenen hello iletişim protokolleri cihaz Bulut ve bulut-cihaz iletişimi ve açılmalıdır hello bağlantı noktası numaraları açıklanmaktadır."
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Başvuru - iletişim protokolü seçin

IOT Hub cihazları toouse sağlayan [MQTT][lnk-mqtt], MQTT WebSockets, üzerinden [AMQP][lnk-amqp], AMQP WebSockets ve HTTP üzerinden iletişim kuralları için cihaz tarafı iletişim. Bu protokollerin belirli IOT Hub özellikleri nasıl desteği hakkında daha fazla bilgi için bkz: [cihaz bulut iletişimleri Kılavuzu] [ lnk-d2c-guidance] ve [bulut-cihaz iletişimi Kılavuzu] [lnk-c2d-guidance].

Merhaba aşağıdaki tabloda hello Protokolü tercih ettiğiniz için üst düzey önerileri sağlar:

| Protokol | Bu protokol seçtiğinizde |
| --- | --- |
| MQTT <br> WebSocket üzerinden MQTT |Tooconnect gerektirmeyen tüm aygıtlarda birden çok aygıt (her kendi cihaz başına kimlik bilgileriyle) hello kullanmak aynı TLS bağlantısı. |
| AMQP <br> AMQP WebSocket üzerinden |Alan ve bulut ağ geçidi tootake avantajlarından aygıtlarda çoğullama bağlantı kullanın. |
| HTTP |Diğer protokolleri destekleyemez cihazlar için kullanın. |

Merhaba cihaz tarafındaki iletişimleri için protokol seçtiğinizde aşağıdaki noktaları göz önünde bulundurun:

* **Bulut cihaz düzeni**. HTTP verimli şekilde tooimplement sunucu itme yok. Bu nedenle, HTTP kullanırken, cihazlar IOT Hub için bulut-cihaz iletilerini yoklar. Bu yaklaşım hello cihaz ve IOT Hub için yetersiz olduğunu. Geçerli HTTP yönergeleri altında her aygıt için iletileri 25 dakikada bir veya daha fazla yoklama. Üzerindeki diğer yandan Merhaba, MQTT ve AMQP sunucu itme bulut-cihaz iletilerini alırken destekler. Bunlar, anında iletileri iter IOT hub'ı toohello aygıttan etkinleştirin. Teslim gecikme ilgili bir sorun varsa, MQTT veya AMQP hello en iyi protokolleri toouse edilir. Nadiren bağlanan cihazlar için HTTP de çalışır.
* **Alan ağ geçitleri**. MQTT ve HTTP kullanırken, birden çok aygıt (her kendi cihaz başına kimlik bilgileriyle) bağlanamıyor kullanarak hello aynı TLS bağlantısı. Bu nedenle, için [alan ağ geçidi senaryoları][lnk-azure-gateway-guidance], her cihaz bağlı toohello alan ağ geçidi için hello alan ağ geçidi ve IOT hub'ı arasında bir TLS bağlantısı gerektirdiğinden bu protokollerin yetersiz.
* **Düşük kaynak aygıtları**. Merhaba MQTT ve HTTP kitaplıkları hello AMQP kitaplıkları daha küçük bir yer vardır. Bu nedenle, Merhaba, cihaz kaynakları (örneğin'den az 1 MB RAM) sınırlıdır, bu protokollere hello yalnızca protokol uygulanması kullanılabilir olabilir.
* **Ağ geçişi**. MQTT kapalı toonon HTTP kurallarıdır ağlarda sorunlara neden olabilecek 8883, bağlantı noktası üzerinde dinleyen sırada bağlantı noktası 5671, hello standart AMQP protokolünü kullanır. Bu senaryoda kullanılan kullanılabilir toobe MQTT WebSockets üzerinden AMQP WebSockets ve HTTP üzerinden olan.
* **Yükü boyutu**. MQTT ve AMQP HTTP değerinden daha küçük yüklerini sonucunda ikili protokoller şunlardır.

> [!WARNING]
> HTTP kullanırken, her cihaz için bulut-cihaz iletilerini 25 dakikada bir veya daha fazla yoklama. Ancak, geliştirme sırasında kabul edilebilir toopoll 25 dakikada daha sık budur.

## Bağlantı noktası numaraları

Aygıtları çeşitli protokoller kullanarak Azure IOT Hub ile iletişim kurabilir. Genellikle, protokol hello seçimi hello belirli gereksinimleri hello çözüm tarafından yönetilir. Hello aşağıdaki tabloda, bir aygıt toobe mümkün toouse için belirli bir iletişim kuralı açılmalıdır hello giden bağlantı noktalarını listeler:

| Protokol | Bağlantı noktası |
| --- | --- |
| MQTT |8883 |
| WebSockets üzerinden MQTT |443 |
| AMQP |5671 |
| AMQP WebSockets üzerinden |443 |
| HTTP |443 |

Bir Azure bölgesinde bir IOT hub oluşturduktan sonra hello IOT hub tutar aynı IP adresini bu IOT hub'ın hello ömrü boyunca hello. Ancak, toomaintain hizmet kalitesi, Microsoft hello IOT hub'ı tooa farklı ölçek birimi sonra onu taşınırsa, yeni bir IP adresi atanır.


## Sonraki adımlar

Merhaba MQTT protokolü, IOT hub'ı nasıl uyguladığını hakkında daha fazla toolearn bkz [hello MQTT protokolünü kullanarak, IOT hub ile iletişim kurun][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
