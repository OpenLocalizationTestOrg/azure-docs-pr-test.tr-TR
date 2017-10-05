---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

## <a name="what-you-will-do"></a>Ne yapacağını

- Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarda çalıştırın.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Gulp aracı IOT hub'ından iletileri okumak için nasıl kullanılır.

## <a name="what-you-need"></a>Ne gerekiyor

- Sanal cihaz örnek [yapılandırma ve çalıştırma sanal cihaz bulut karşıya örnek uygulama](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma

Cihaz bağlantı dizesi, IOT hub'ınıza bağlanmak için sanal cihazınız tarafından kullanılır. IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır.

- Kaynak grubunuzdaki tüm IOT hub aşağıdaki komutu çalıştırarak listesi:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Kullanım `iot-gateway` değeri olarak `{resource group name}` onu değiştirilmediyse.
- IOT hub bağlantı dizesine, aşağıdaki komutu çalıştırarak alın:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`Ders 2'de belirtilen adıdır.

## <a name="configure-the-device-connection-for-the-sample-code"></a>Örnek kod için cihaz bağlantısı

IOT hub ve cihaz bağlantısı yapılandırmalarını güncelleştirme `config-azure.json` aşağıdaki adımları gerçekleştirerek:

1. Açık `config-azure.json` Visual Studio konsol penceresinde aşağıdaki komutu çalıştırarak kod:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. İçinde aşağıdaki değişiklikleri yapın `config-azure.json` dosyası:

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Değiştir `[IoT hub connection string]` IOT hub bağlantı dizesine sahip.

## <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

Sanal cihaz örnek uygulamayı çalıştırın ve IOT Hub aşağıdaki komutla iletilerini okuyun:

```bash
gulp run --iot-hub
```

Komut iletileri 2 saniyede IOT hub'ınıza gönderir uygulama çalışır. İleti almak için bir alt işlem olarak çoğaltılır.

Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir. Uygulama 40 saniye cinsinden çıkılacak.

![Gönderilen ve alınan ileti ile sanal örnek uygulama](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Özet

İle sanal cihaz IOT hub'ınıza veri göndermek için örnek uygulama başarıyla çalıştırdıysanız. Ayrıca, IOT hub'a gönderilen iletileri okuduğunuz.

## <a name="next-steps"></a>Sonraki adımlar
[Azure işlev uygulaması ve Azure Depolama hesabı oluşturma](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


