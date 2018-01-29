---
title: "Azure IOT Hub Mesajlaşma anlama | Microsoft Docs"
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
ms.date: 09/14/2017
ms.author: dobett
ms.openlocfilehash: 4a7f545f1af2904f47808fe8b1d7d3aab3afff84
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/18/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Cihaz Bulut ve bulut-cihaz IOT Hub ile Mesajlaşma

IOT Hub'ın cihazlar tarafından ile iletişim kurmak için Mesajlaşma kullanın:

* Gönderme [cihaz bulut] [ lnk-d2c] cihazlarınızdan gelen iletileri çözümünüze son yedekleme.
* Gönderme [bulut cihaz] [ lnk-c2d] çözümü iletilerden aygıtlarınıza son yedekleme.

Çekirdek IOT hub'ı Mesajlaşma işlevleri güvenilirlik ve dayanıklılık iletilerinin özellikleridir. Bu özellikleri aralıklı bağlantısı cihaz tarafındaki ve olay bulut tarafında işleme ani yüklemek için esneklik sağlar. IOT hub'ı uygulayan *en az bir kez* teslim cihaz Bulut ve bulut-cihaz Mesajlaşma güvence altına alır.

Giriş IOT hub için özellikleri makalelerine bakın [Azure ve nesnelerin interneti] [ lnk-azure-iot] ve [Azure IOT Hub hizmetine genel bakış][lnk-iot-hub-overview].

## <a name="when-to-use-iot-hub-messaging"></a>IOT Hub'ın Mesajlaşma kullanma zamanı

Zaman serisi telemetri ve uyarılar, cihaz uygulamanızdan göndermek için cihaz bulut iletilerini ve bulut-cihaz iletilerini cihaz uygulamanız için tek yönlü bildirimler için kullanın.

* Başvurmak [cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] IF cihaz bulut iletilerini, bildirilen özellikleri veya karşıya dosya yükleme kullanarak arasında şüpheli.
* Başvurmak [bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] IF bulut-cihaz iletilerini, istenen özelliklerini veya doğrudan yöntemlerini kullanarak arasında şüpheli.

## <a name="next-steps"></a>Sonraki adımlar

* IOT Hub hakkında bilgi edinin [cihaz bulut Mesajlaşma][lnk-d2c].
* IOT Hub hakkında bilgi edinin [bulut cihaz Mesajlaşma][lnk-c2d].

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md