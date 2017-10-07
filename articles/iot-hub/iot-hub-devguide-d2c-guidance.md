---
title: "aaaAzure IOT hub'a cihaz-bulut seçenekleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - ne zaman toouse cihaz bulut iletilerini, bildirilen özellikleri ya da dosya karşıya yükleme bulut-cihaz iletişimi için yönergeler."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Cihaz bulut iletişimleri Kılavuzu
Merhaba cihaz uygulama toohello çözüm arka uçtan bilgi gönderirken, IOT hub'ı üç seçenek sunar:

* [Cihaz bulut iletilerini] [ lnk-d2c] zaman serisi telemetri ve Uyarılar için.
* [Özellikler bildirilen] [ lnk-twins] kullanılabilir özellikleri, koşullar veya uzun süre çalışan iş akışları hello durumu gibi cihaz durumu bilgilerini raporlama. Örneğin, yapılandırma ve yazılım güncelleştirmeleri.
* [Dosya yüklemeleri] [ lnk-fileupload] ortam dosyaları ve büyük telemetri toplu aralıklı bağlı cihazlar tarafından karşıya veya sıkıştırılmış toosave bant genişliği.

Çeşitli cihaz bulut iletişim seçenekleri hello ayrıntılı bir karşılaştırmasını aşağıdadır.

|  | Cihazdan buluta iletiler | Bildirilen özellikleri | Dosya yüklemeleri |
| ---- | ------- | ---------- | ---- |
| Senaryo | Telemetri zaman serisi ve Uyarıları. Örneğin, 5 dakikada 256 KB algılayıcı veri yığını gönderdi. | Kullanılabilir özellikler ve koşulları. Örneğin, hello geçerli cihaz bağlantı modunu cep gibi veya WiFi. Uzun süre çalışan iş akışları, yapılandırma ve yazılım güncelleştirmeleri gibi eşitleniyor. | Ortam dosyaları. Büyük (genellikle sıkıştırılmış) telemetri toplu işler. |
| Depolama ve alma | Geçici olarak IOT Hub tarafından too7 günleri depolanır. Yalnızca sıralı okuma. | IOT Hub tarafından hello cihaz çiftine depolanır. Alınabilir hello kullanarak [IOT hub'ı sorgu dili][lnk-query]. | Kullanıcı tarafından sağlanan Azure depolama hesabında depolanır. |
| Boyut | Too256 KB iletileri. | En fazla bildirilen özellikleri boyutu 8 KB'tır. | Azure Blob Storage tarafından desteklenen en büyük dosya boyutu. |
| Sıklık | Yüksek. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. | Orta. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. | Düşük. Daha fazla bilgi için bkz: [IOT hub'ı sınırlar][lnk-quotas]. |
| Protokol | Tüm protokoller kullanılabilir. | Şu anda yalnızca MQTT kullanırken kullanılabilir. | Herhangi bir protokolünü kullanarak ancak gerektirdiğinde HTTP hello aygıtta kullanılabilir. |

Bir uygulama tooboth gönderme bir telemetri zaman serisi veya uyarı ve bilgileri de toomake gerektirdiğini mümkündür, hello cihaz çiftine kullanılabilir. Bu senaryoda, aşağıdaki seçenekleri şu Merhaba, seçtiğiniz yapabilirsiniz:

* Merhaba cihaz uygulaması cihaz bulut ileti gönderir ve özellik değişikliği raporlar.
* Merhaba iletisi aldığında hello çözüm arka ucu hello cihaz çifti'nın etiketlerinde hello bilgi depolayabilir.

Cihaz çifti güncelleştirmeleri daha bir çok daha yüksek verimlilik cihaz bulut iletilerini etkinleştir olduğundan, bazen arzu tooavoid güncelleştirme hello cihaz çifti her cihaz bulut ileti kalır.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
