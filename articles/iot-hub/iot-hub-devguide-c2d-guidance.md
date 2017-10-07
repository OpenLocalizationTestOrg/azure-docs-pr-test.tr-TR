---
title: "aaaAzure IOT hub'ı bulut-cihaz seçenekleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - toouse zaman doğrudan yöntemleri, cihaz çifti'nin istediğiniz özellikler veya Bulut-cihaz iletilerini bulut-cihaz iletişimi için yönergeler."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Bulut-cihaz iletişimi Kılavuzu
IOT Hub cihaz uygulamaları tooexpose işlevselliği tooa arka uç uygulaması için üç seçenek sunar:

* [Doğrudan yöntemleri] [ lnk-methods] hello sonucunun hemen onay gerektiren iletişimleri için. Doğrudan yöntemleri genellikle üzerinde fan kapatma gibi aygıtların etkileşimli denetimi için kullanılır.
* [Twin özellikleri istenen] [ lnk-twins] uzun süre çalışan komutlar belirli bir tooput hello cihazda istenen durum amaçlar için. Örneğin, hello telemetri gönderme aralığı too30 dakika olarak ayarlayın.
* [Bulut-cihaz iletilerini] [ lnk-c2d] tek yönlü bildirimleri toohello cihaz uygulaması için.

Çeşitli bulut-cihaz iletişimi seçenekleri hello ayrıntılı bir karşılaştırmasını aşağıdadır.

|  | Doğrudan yöntemler | Twin'ın istenen özellikleri | Bulut-cihaz iletilerini |
| ---- | ------- | ---------- | ---- |
| Senaryo | Fan üzerinde kapatma gibi hemen onay gerektiren komutlar. | Uzun süre çalışan komutlar tooput hello aygıt bir belirli istenen duruma amaçlanmıştır. Örneğin, hello telemetri gönderme aralığı too30 dakika olarak ayarlayın. | Tek yönlü bildirimleri toohello cihaz uygulaması. |
| Veri akışı | İki yönlü. Merhaba cihaz uygulaması toohello yöntemi hemen yanıt verebilir. Merhaba çözüm arka ucu alır hello sonucu bağlam toohello isteği. | Tek yönlü. Merhaba cihaz uygulaması hello özellik değişikliği içeren bir bildirim alır. | Tek yönlü. Merhaba ileti Hello cihaz uygulaması alır
| Dayanıklılık | Bağlantısı kesilmiş aygıtları temas değil. Merhaba çözüm arka ucu hello aygıt bağlanmamış bildirilir. | Özellik değerlerini hello cihaz çiftine korunur. Aygıt, sonraki yeniden bağlanma sırasında okuyun. Özellik değerleri ile Merhaba alınabilir [IOT hub'ı sorgu dili][lnk-query]. | İletileri too48 saatleri için IOT Hub tarafından korunabilir. |
| Hedefleri | Tek bir cihazla **DeviceID**, veya birden çok cihazı kullanarak [işleri][lnk-jobs]. | Tek bir cihazla **DeviceID**, veya birden çok cihazı kullanarak [işleri][lnk-jobs]. | Tek aygıt tarafından **DeviceID**. |
| Boyut | Too8KB istekleri ve 8 KB yanıtları. | Maksimum özellikleri boyutu 8 KB istenen. | Too64KB iletileri. |
| Sıklık | Yüksek. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. | Orta. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. | Düşük. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. |
| Protokol | Şu anda yalnızca MQTT kullanırken kullanılabilir. | Şu anda yalnızca MQTT kullanırken kullanılabilir. | Tüm protokoller kullanılabilir. Cihaz HTTP kullanırken yoklaması gerekir. |

Nasıl toouse doğrudan yöntemler, istenen özellikler ve bulut-cihaz iletilerini öğreticileri aşağıdaki hello öğrenin:

* [Doğrudan yöntemleri kullanın][lnk-methods-tutorial], doğrudan yöntemleri;
* [İstenen özelliklerde tooconfigure aygıtları kullanan][lnk-twin-properties], cihaz çifti özellikleri; istenen için 
* [Bulut-cihaz iletilerini göndermek][lnk-c2d-tutorial], bulut cihaz iletileri için.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
