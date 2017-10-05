---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "IOT hub'ınıza sıcaklık veri göndermek için bir sanal cihaz örnek uygulamayı çalıştırma"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Bulut için veri"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Yapılandırma ve sanal cihaz örnek uygulamayı çalıştırma

## <a name="what-you-will-do"></a>Ne yapacağını

- Örnek depoyu kopyalayın.
- IOT hub ve sanal cihaz örnek uygulama için mantıksal aygıt bilgilerini almak için Azure CLI kullanın. Yapılandırın ve sanal cihaz örnek uygulamayı çalıştırın.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu makalede, şunları öğreneceksiniz:

- Nasıl yapılandırmak ve sanal cihaz örnek uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor

Başarılı bir şekilde tamamladınız gerekir

- [IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Ana bilgisayara örnek depoyu kopyalayın

Örnek deposuna kopyalamak için ana bilgisayarda aşağıdaki adımları izleyin:

1. Windows komut istemi veya terminal macOS veya Ubuntu açın.
2. Aşağıdaki komutları çalıştırın:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a>Sanal cihazı ve, NUC yapılandırın

1. Yapılandırma dosyasını açın `config.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   code config.json
   ```

2. Değiştir `"has_sensortag": true` ile`"has_sensortag": false`

   ![Config tı SensorTag cihaz yok](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Açık `config-gateway.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Aşağıdaki kod satırını bulun ve değiştirin `[device hostname or IP address]` Intel NUC IP adresi veya ana bilgisayar adına sahip.
   ![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a>IOT hub mantıksal aygıtı bağlantı dizesi alma

Mantıksal Cihazınızı Azure IOT hub bağlantı dizesini almak için ana bilgisayarda aşağıdaki komutu çalıştırın:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`kullandığınız IOT hub addır. IOT ağ geçidi değeri olarak kullanın `{resource group name}` ve mydevice değeri olarak `{device id}` Ders 2 değerinde değiştirilmediyse.

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a>Sanal cihaz bulut karşıya yükleme örnek uygulamayı yapılandırma

Yapılandırmak ve sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:

1. Açık `config-sensortag.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Kod içinde aşağıdaki değişiklikleri yapın:
   - Değiştir `[IoT hub name]` IOT hub'ı adı ile.
   - Değiştir `[IoT device connection string]` IOT hub mantıksal aygıtı bağlantı dizesi ile.

3. Uygulamayı çalıştırın.

   Dağıtma ve aşağıdaki komutu çalıştırarak uygulamayı çalıştırın:

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a>Örnek uygulama çalıştığını doğrulama

Şimdi aşağıdaki gibi bir çıktı görmeniz gerekir:

![Sanal cihaz örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

Uygulama için 40 saniye sürer, IOT hub ' ınızı sıcaklık verileri gönderir.

## <a name="summary"></a>Özet

Başarılı bir şekilde yapılandırılmış artık ve veri ile sanal cihaz IOT hub'ınıza gönderen sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ınızdan ileti okuma](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)