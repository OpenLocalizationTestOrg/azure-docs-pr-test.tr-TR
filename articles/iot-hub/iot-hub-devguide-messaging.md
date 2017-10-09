---
title: "Azure IOT Hub aaaUnderstand Mesajlaşma | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihaz Bulut ve bulut-cihaz IOT Hub ile ileti. İleti biçimleri ve desteklenen protokolleri hakkında bilgi içerir."
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Cihaz Bulut ve bulut-cihaz IOT Hub ile Mesajlaşma

IOT Hub'ın cihazlar tarafından ile toocommunicate Mesajlaşma kullanın:

* Gönderme [cihaz bulut] [ lnk-d2c] aygıtları tooyour çözümünüzü iletilerden son yedekleme.
* Gönderme [bulut cihaz] [ lnk-c2d] hello çözüm arka iletilerden bitiş tooyour aygıtlar.

Çekirdek IOT hub'ı Mesajlaşma işlevleri hello güvenilirlik ve dayanıklılık iletilerinin özellikleridir. Bu özellikleri hello cihaz tarafındaki esnekliği toointermittent bağlantıyı etkinleştirmek ve hello bulut tarafında işleme olay tooload ani. IOT hub'ı uygulayan *en az bir kez* teslim cihaz Bulut ve bulut-cihaz Mesajlaşma güvence altına alır.

İçin bir giriş toohello özellikleri IOT Hub'ının hello makalelerine bakın [Azure ve nesnelerin interneti] [ lnk-azure-iot] ve [hello Azure IOT Hub hizmetine genel bakış] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Zaman toouse IOT hub'ı Mesajlaşma

Zaman serisi telemetri ve uyarılar, cihaz uygulamanızdan göndermek için cihaz bulut iletilerini ve bulut-cihaz iletilerini tek yönlü bildirimleri tooyour aygıt uygulama için kullanın.

* Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] IF cihaz bulut iletilerini, bildirilen özellikleri veya karşıya dosya yükleme kullanarak arasında şüpheli.
* Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] IF bulut-cihaz iletilerini, istenen özelliklerini veya doğrudan yöntemlerini kullanarak arasında şüpheli.

## <a name="next-steps"></a>Sonraki adımlar

* IOT Hub hakkında bilgi edinin [cihaz bulut Mesajlaşma][lnk-d2c].
* IOT Hub hakkında bilgi edinin [bulut cihaz Mesajlaşma][lnk-c2d].

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md