---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından ana bilgisayar tooread hello iletilerde çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

## <a name="what-you-will-do"></a>Ne yapacağını

- Örnek kod, IOT hub'ından bilgisayar tooread iletileri ana bilgisayarda çalıştırın.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Nasıl toouse hello aracı tooread IOT hub'ınızı iletilerden gulp.

## <a name="what-you-need"></a>Ne gerekiyor

- Merhaba sanal cihaz örnek [yapılandırma ve çalıştırma sanal cihaz bulut karşıya örnek uygulama](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma

Merhaba cihaz bağlantı dizesi, sanal cihaz tooconnect tooyour IOT hub tarafından kullanılır. Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir.

- Kaynak grubunuzdaki tüm IOT hub hello aşağıdaki komutu çalıştırarak listesi:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Kullanım `iot-gateway` hello değeri olarak `{resource group name}` onu değiştirilmediyse.
- Hello IOT hub bağlantı dizesine hello aşağıdaki komutu çalıştırarak alın:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`Ders 2'de belirtilen hello adıdır.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Merhaba cihaz bağlantısı hello örnek kod için yapılandırma

IOT hub ve cihaz bağlantısı yapılandırmalarını güncelleştirme `config-azure.json` hello aşağıdaki adımları gerçekleştirerek:

1. Açık `config-azure.json` komutu bir konsol penceresinde aşağıdaki hello çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Merhaba değişikliklerini aşağıdaki hello olun `config-azure.json` dosyası:

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Değiştir `[IoT hub connection string]` hello IOT hub bağlantı dizesine sahip.

## <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

Benzetimli hello aygıt örnek uygulamayı çalıştırın ve IOT Hub tarafından komutu aşağıdaki hello iletilerini okuyun:

```bash
gulp run --iot-hub
```

Merhaba komutu 2 saniyede tooyour IOT hub'ı iletileri gönderir Merhaba uygulaması çalıştırır. Bir alt işlem tooreceive selamlama iletisine olarak çoğaltılır.

gönderilen ve alınan tüm hizmetlerde Anında hello aynı konsol penceresinde hello iletileri ana makine hello. Merhaba uygulaması 40 saniye cinsinden çıkılacak.

![Gönderilen ve alınan ileti ile sanal örnek uygulama](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Özet

Sanal cihaz ile Merhaba örnek uygulama toosend veri tooyour IOT hub'ı başarıyla çalıştırdıysanız. Ayrıca tooyour IOT hub gönderilen Merhaba iletileri okuduğunuz.

## <a name="next-steps"></a>Sonraki adımlar
[Azure işlev uygulaması ve Azure Depolama hesabı oluşturma](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


