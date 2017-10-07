---
title: "IOT hub'ı aaaAzure ölçeklendirme | Microsoft Docs"
description: "Nasıl tooscale IOT hub toosupport beklenen ileti işleme. Her katman için desteklenen hello verimliliği ve parçalama seçeneklerini özetini içerir."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>IOT hub çözümünüzü ölçeklendirme
Azure IOT Hub tooa milyon aynı anda bağlı cihazları destekler. Daha fazla bilgi için bkz: [IOT Hub'ın fiyatlandırma][lnk-pricing]. Her IOT hub'ı birimi belirli sayıda günlük iletileri izin verir.

tooproperly çözümünüzü ölçeklendirme, belirli IOT hub'ı kullanımınızı göz önünde bulundurun. Özellikle, kategoriler işlemlerinin aşağıdaki hello için gerekli hello en yüksek işleme göz önünde bulundurun:

* Cihazdan buluta iletiler
* Bulut-cihaz iletilerini
* Kimlik kayıt defteri işlemleri

Toplama toothis üretilen iş bilgilerine bakın [IOT hub'ı kotaları ve kısıtlamaları] [ IoT Hub quotas and throttles] ve çözümünüzün uygun şekilde tasarlayın.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Cihaz Bulut ve bulut-cihaz ileti işleme
Merhaba en iyi şekilde toosize IOT hub'ı çözümünü tooevaluate hello birim başına temelinde trafiğidir.

Cihaz bulut iletilerini bu aralıksız üretilen yönergeleri izleyin.

| Katman | Aralıksız üretilen | Sürdürülen gönderme oranı |
| --- | --- | --- |
| S1 |Too1111 KB dakikada birim başına<br/>(1,5 GB/gün/birim) |278 iletileri dakikada birim başına ortalama<br/>(400.000 iletileri/gün birim başına) |
| S2 |Too16 MB dakikada birim başına<br/>(22.8 GB/gün/birim) |4,167 iletileri dakikada birim başına ortalama<br/>(6 milyon iletileri/gün birim başına) |
| S3 |Too814 MB dakikada birim başına<br/>(1144.4 GB/gün/birim) |208,333 iletileri dakikada birim başına ortalama<br/>(300 milyon iletileri/gün birim başına) |

## <a name="identity-registry-operation-throughput"></a>Kimlik kayıt defteri işlemi işleme
Bunlar çoğunlukla ilgili toodevice sağlama olduğu IOT Hub kimlik kayıt defteri işlemlerini toobe çalıştırma işlemleri, beklenen değil.

Belirli veri bloğu performans numaraları için bkz: [IOT hub'ı kotaları ve kısıtlamaları][IoT Hub quotas and throttles].

## <a name="sharding"></a>Parçalama
Bazen tek bir IOT hub cihaz toomillions ölçeklendirebilirsiniz olmakla birlikte, çözümünüzü tek bir IOT hub garanti edemez özel performans özellikleri gerektirir. Bu durumda, birden çok IOT hub'ları aygıtlarınızı bölüm önerilir. Birden çok IOT hub'ları trafiği WINS'e kesintisiz ve hello gerekli işleme veya gerekli işlem hızları elde edin.

## <a name="next-steps"></a>Sonraki adımlar
toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
