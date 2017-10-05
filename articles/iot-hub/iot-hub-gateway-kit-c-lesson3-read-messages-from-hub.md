---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

## <a name="what-you-will-do"></a>Ne yapacağını

- Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarda çalıştırın.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Gulp aracı IOT hub'ından iletileri okumak için nasıl kullanılır.

## <a name="what-you-need"></a>Ne gerekiyor

- Ders 3'te başarıyla çalıştırıldığını bırak örnek uygulama.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma

Cihaz bağlantı dizesi (tı SensorTag veya sanal cihaz) IOT hub'ınıza bağlanmak için aygıt tarafından kullanılır. IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır.

- Kaynak grubunuzdaki tüm IOT hub aşağıdaki komutu çalıştırarak listesi:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Kullanım `iot-gateway` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.
- IOT hub bağlantı dizesine, aşağıdaki komutu çalıştırarak alın:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`Ders 2'de belirtilen adıdır.

## <a name="configure-the-device-connection-for-the-sample-code"></a>Örnek kod için cihaz bağlantısı

Aygıt yapılandırma dosyasını güncelleştirme `config-azure.json` böylece IOT hub'ından ana bilgisayarınızda iletileri okuyabilir. Bunu yapmak için aşağıdaki adımları izleyin:

1. Açık `config-azure.json` Visual Studio konsol penceresinde aşağıdaki komutu çalıştırarak kod:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. İçinde aşağıdaki değişiklikleri yapın `config-azure.json` dosyası:

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Değiştir `[IoT hub connection string]` aldığınız IOT hub bağlantı dizesine sahip.

## <a name="read-messages-from-your-iot-hub"></a>IOT hub'ından iletilerini okuyun

TI SensorTag varsa, SensorTag üzerinde zaten açık emin olun. Ağ geçidi örnek uygulamayı çalıştırın ve IOT Hub aşağıdaki komutla iletilerini okuyun:

```bash
gulp run --iot-hub
```

Komutu okuyan ve SensorTag veya sanal cihaz sıcaklık verileri paketleri ve iletiyi 2 saniyede IOT hub'ınıza gönderir bırak örnek uygulamayı çalıştırır. İleti almak için bir alt işlem olarak çoğaltılır.

Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir. Örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.

![BIRAK örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Özet

IOT hub'ından iletileri okumak için örnek kod çalıştırdıysanız. Azure table storage'da depolanan iletileri okumak hazırsınız.

## <a name="next-steps"></a>Sonraki adımlar
[Azure işlev uygulaması ve Azure Depolama hesabı oluşturma](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


