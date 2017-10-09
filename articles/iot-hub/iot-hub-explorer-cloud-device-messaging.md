---
title: "iothub-Gezgini ile Mesajlaşma aaaManage Azure IOT Hub bulut cihaz | Microsoft Docs"
description: "Nasıl toouse iothub-explorer CLI aracı toomonitor aygıt toocloud (D2C) iletilerini hello bulut toodevice (C2D) iletileri ve Azure IOT hub'da gönderme öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "ıothub Gezgini, Mesajlaşma, bulut cihaz IOT hub bulut toodevice, bulut toodevice Mesajlaşma"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Aygıt ve IOT hub'ı arasında ileti alıp ıothub explorer toosend kullanın

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[ıothub explorer](https://github.com/azure/iothub-explorer) IOT hub'ı yönetimini kolaylaştırır komutları sayıda sahiptir. Bu öğretici odaklanılmaktadır toouse iothub-explorer toosend Cihazınızı ve IOT hub'ınız arasında ileti alıp.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Hakkında bilgi edineceksiniz nasıl toouse iothub-explorer toomonitor cihaz bulut iletilerini ve toosend bulut-cihaz iletilerini. Cihaz bulut iletilerini Cihazınızı toplar ve tooyour IOT hub'ı gönderir algılayıcı verilerini olabilir. Bulut-cihaz iletilerini IOT hub'ınızı bağlı tooyour aygıt bir LED tooyour aygıt tooblink gönderir komutları olabilir.

## <a name="what-you-will-do"></a>Ne yapacağını

- Iothub explorer toomonitor cihaz bulut iletilerini kullanın.
- Iothub explorer toosend bulut-cihaz iletilerini kullanın.

## <a name="what-you-need"></a>Ne gerekiyor

- Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:
  - Etkin bir Azure aboneliği.
  - Azure IOT hub'ı aboneliğinizdeki.
  - Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.
- iothub-Gezgini. ([Yükleme ıothub explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Cihaz bulut iletilerini izleme

cihaz tooyour IOT hub'dan gönderilen toomonitor iletileri şu adımları izleyin:

1. Bir konsol penceresi açın.
1. Merhaba aşağıdaki komutu çalıştırın:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Alma `<device-id>` ve `<IoTHubConnectionString>` IOT hub'ınızı gelen. Emin olun hello önceki öğreticiyi bitirdikten sonra. Ya da toouse deneyebilirsiniz `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` varsa `HostName`, `SharedAccessKeyName` ve `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Buluttan cihaza iletileri gönderme

toosend IOT hub tooyour cihazı iletiden şu adımları izleyin:

1. Bir konsol penceresi açın.
1. Bir oturum hello aşağıdaki komutu çalıştırarak, IOT hub'ına başlatın:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Bir ileti tooyour aygıt hello aşağıdaki komutu çalıştırarak gönder:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

Merhaba komutu bağlı tooyour cihaz ve hello ileti tooyour cihaz gönderen hello ışığı yanıp.

> [!Note]
> Merhaba iletiyi aldıktan sonra ayrı ack komutu geri tooyour IOT hub hello aygıt toosend için gerek yoktur.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toomonitor cihaz-bulut iletileri ve bulut-cihaz iletilerini IOT cihaz ile Azure IOT hub'ı arasında göndermek öğrendiniz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
