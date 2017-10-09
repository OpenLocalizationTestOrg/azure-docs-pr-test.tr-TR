---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "Bir sanal cihaz örnek uygulama toosend sıcaklık veri tooyour IOT hub çalıştırın"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Veri toocloud
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Yapılandırma ve sanal cihaz örnek uygulamayı çalıştırma

## <a name="what-you-will-do"></a>Ne yapacağını

- Kopya hello örnek depo.
- Hello Azure CLI tooget sanal cihaz örnek bir uygulama için IOT hub ve mantıksal aygıt bilgileri kullanın. Yapılandırma ve benzetimli hello aygıt örnek uygulamayı çalıştırın.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu makalede, şunları öğreneceksiniz:

- Nasıl tooconfigure ve çalışma hello aygıt örnek uygulama benzetimi.

## <a name="what-you-need"></a>Ne gerekiyor

Başarılı bir şekilde tamamladınız gerekir

- [IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Kopya hello örnek depo toohello ana bilgisayarı

tooclone hello örnek deposu, hello ana bilgisayarda aşağıdaki adımları izleyin:

1. Windows komut istemi veya terminal macOS veya Ubuntu açın.
2. Merhaba aşağıdaki komutları çalıştırın:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Merhaba sanal cihazı ve, NUC yapılandırın

1. Açık hello yapılandırma dosyası `config.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   code config.json
   ```

2. Değiştir `"has_sensortag": true` ile`"has_sensortag": false`

   ![Config tı SensorTag cihaz yok](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Açık `config-gateway.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Aşağıdaki kod hello bulun ve değiştirin `[device hostname or IP address]` hello Intel NUC IP adresi veya ana bilgisayar adına sahip.
   ![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>IOT hub mantıksal aygıtı Hello bağlantı dizesi alma

tooget hello Azure IOT hub bağlantı dizesine hello ana bilgisayarda komut aşağıdaki hello çalıştırmak aygıtınızın mantıksal:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`kullandığınız hello IOT hub adıdır. IOT ağ geçidi hello değeri olarak kullanın `{resource group name}` ve mydevice hello değeri olarak `{device id}` Ders 2 hello değerinde değiştirilmediyse.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Benzetimli hello cihaz bulut karşıya yükleme örnek uygulamayı yapılandırma

tooconfigure ve benzetimli çalışma hello cihaz bulut örnek uygulamayı karşıya yüklemek, hello ana bilgisayarda aşağıdaki adımları izleyin:

1. Açık `config-sensortag.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Merhaba kodda değişiklik aşağıdaki hello olun:
   - Değiştir `[IoT hub name]` hello IOT hub'ı adı ile.
   - Değiştir `[IoT device connection string]` IOT hub'ı mantıksal aygıtınızın hello bağlantı dizesiyle.

3. Merhaba uygulamayı çalıştırın.

   Dağıtma ve hello aşağıdaki komutu çalıştırarak hello uygulamayı çalıştırın:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Merhaba örnek uygulama çalıştığını doğrulama

Şimdi hello aşağıdaki gibi bir çıktı görmeniz gerekir:

![Sanal cihaz örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

Merhaba uygulaması, 40 saniye sürer sıcaklık veri tooyour IOT hub'ına gönderir.

## <a name="summary"></a>Özet

Başarılı bir şekilde yapılandırdıysanız ve veri tooyour IOT hub ile sanal cihaz gönderen cihaz bulut karşıya yükleme örnek uygulamayı çalıştırma hello benzetimli.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ınızdan ileti okuma](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)