---
title: "aaaAzure iothub-explorer ile IOT cihaz Yönetimi | Microsoft Docs"
description: "Merhaba ıothub explorer CLI aracı hello doğrudan yöntemleri ve hello Twin'ın istenen özellikleri yönetim seçenekleri özelliklerine sahip Azure IOT Hub cihaz yönetimi için kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT cihaz yönetimi, azure IOT hub cihaz yönetimi, cihaz yönetim IOT, IOT hub cihaz Yönetimi"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Azure IOT Hub cihaz yönetimi için ıothub explorer'ı kullanın

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[ıothub explorer](https://github.com/azure/iothub-explorer) IOT hub kayıt defterinizde bir ana bilgisayar toomanage cihaz kimliklerini çalıştırdığınız bir CLI aracıdır. Çeşitli görevleri tooperform kullanabileceğiniz yönetim seçenekleri ile birlikte gelir.

| Yönetim seçeneği          | Görev                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Doğrudan yöntemler             | Başlatma veya ileti gönderme veya hello cihaz yeniden başlatıldığı durdurma gibi davranacak bir aygıtı olun.                                        |
| İstenen twin özellikleri    | Bir aygıt LED toogreen ayarlama gibi bazı durumların yerleştirin veya hello telemetri ayarı aralığı too30 dakika gönderin.         |
| Özellikler Twin bildirdi   | Alma hello aygıtın durumunu bildirdi. Örneğin, hello aygıt LED şimdi yanıp sönen hello bildirir.                                    |
| Twin etiketleri                  | Aygıta özgü meta veriler hello bulutta depolayın. Örneğin, bir satış makinenin dağıtım konumu hello.                         |
| Bulut-cihaz iletilerini   | Bildirimleri tooa aygıt gönderin. Örneğin, "Bu büyük olasılıkla toorain bugün olur. Toobring bir şemsiyesi unutmayın."              |
| Cihaz çifti sorguları        | Tüm cihaz çiftlerini tooretrieve olanlar gibi kullanılabilir hello aygıtlarını tanımlayan rasgele koşullarla sorgu. |

Daha ayrıntılı açıklama hello farklar hakkında ve bu seçenekleri kullanma konusunda yönergeler için bkz: [cihaz bulut iletişimi Kılavuzu](iot-hub-devguide-d2c-guidance.md) ve [bulut-cihaz iletişimi Kılavuzu](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir. IOT Hub cihaz çifti tooit bağlanan her aygıt için devam ettirir. Cihaz çiftlerini hakkında daha fazla bilgi için bkz: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Öğrenecekleriniz

Geliştirme makinenizde çeşitli yönetim seçenekleri ile ıothub explorer'ı kullanarak öğrenin.

## <a name="what-you-do"></a>Neler

Iothub explorer çeşitli yönetim seçenekleri ile çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor

- Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:
  - Etkin bir Azure aboneliği.
  - Azure IOT hub'ı aboneliğinizdeki.
  - Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.
- Cihazınızı Merhaba istemci uygulaması Bu öğretici sırasında çalıştırdığından emin olun.
- iothub-explorer [yükleme ıothub explorer](https://github.com/azure/iothub-explorer) geliştirme makinenizde.

## <a name="connect-tooyour-iot-hub"></a>Tooyour IOT hub'ı Bağlan

Tooyour IOT hub'ı hello aşağıdaki komutu çalıştırarak Bağlan:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Doğrudan yöntemleriyle ıothub Gezgini'ni kullanın

Merhaba çağırma `start` hello aşağıdaki komutu çalıştırarak hello cihaz uygulama toosend iletileri tooyour IOT hub yöntemi:

```bash
iothub-explorer device-method <your device Id> start
```

Merhaba çağırma `stop` hello cihaz uygulama toostop gönderme yöntemi hello aşağıdaki komutu çalıştırarak tooyour IOT hub'ı iletileri:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Twin'ın istenen özelliklere sahip ıothub Gezgini'ni kullanın

İstenen özellik aralığı ayarlamak hello aşağıdaki komutu çalıştırarak 3000 =:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Bu özellik, cihazınız tarafından okunabilir.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Twin'ın bildirilen özelliklerle ıothub Gezgini'ni kullanın

Merhaba bildirilen hello çalıştırarak hello cihazın komutu aşağıdaki özelliklere alın:

```bash
iothub-explorer get-twin <your device id>
```

$Metadata hello özellikleri biridir. hangi gösterir, bu aygıtın son zamanı hello $lastUpdated gönderir veya bir ileti alır.

## <a name="use-iothub-explorer-with-twins-tags"></a>Twin'ın etiketleriyle ıothub Gezgini'ni kullanın

Başlangıç etiketleri ve hello cihaz özelliklerini hello aşağıdaki komutu çalıştırarak görüntüler:

```bash
iothub-explorer get-twin <your device id>
```

Bir alan rolü eklemek hello aşağıdaki komutu çalıştırarak = sıcaklık ve nem toohello cihazın:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Bulut cihaza iletileriyle ıothub Gezgini'ni kullanın

"Hello World" iletisini toohello aygıt hello aşağıdaki komutu çalıştırarak gönder:

```bash
iothub-explorer send <device-id> "Hello World"
```

Bkz: [iothub-explorer toosend kullanıyorsanız ve cihaz ve IOT hub'ı arasında iletileri alırsanız](iot-hub-explorer-cloud-device-messaging.md) bu komutu kullanarak, gerçek bir senaryo için.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Cihaz çiftlerini sorgularıyla ıothub Gezgini'ni kullanın

Sorgu bir etiket rolünün aygıtlarla 'sıcaklık ve nem' hello aşağıdaki komutu çalıştırarak =:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Bir etiketi rolünün olanlar dışında tüm cihazlar sorgu 'sıcaklık ve nem' hello aşağıdaki komutu çalıştırarak =:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Sonraki adımlar

Öğrendiğinize nasıl toouse iothub-Gezgini çeşitli yönetim seçenekleri ile.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
