---
title: "Azure IOT - Ders 1 Arduino bağlanın: uygulama dağıtma | Microsoft Docs"
description: "GitHub örnek Arduino uygulamadan kopyalama ve Adafruit yumuşatma M0 WiFi bu uygulamayı dağıtmak için gulp çalıştırın. Bu örnek uygulama GPIO'yu yanıp"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projeleri arduino neden, arduino öncülük blink, neden arduino blink kodunu arduino blink programı, arduino blink örneği"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Blink uygulaması oluşturma ve dağıtma
## <a name="what-you-will-do"></a>Ne yapacağını
GitHub örnek Arduino uygulamadan kopyalama ve Adafruit yumuşatma M0 WiFi Arduino panonuzu örnek uygulamayı dağıtmak için gulp aracını kullanın. Örnek uygulama yanıp sönme GPIO'yu #13 üzerinde-barod her iki saniye GEREKTİRİYORDU.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting-page].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
* Nasıl dağıtmak ve Arduino Panonuzda örnek uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor
Aşağıdaki işlemleri başarıyla tamamlandı gerekir:

* [Cihazınızı yapılandırın][configure-your-device]
* [Araçları edinin][get-the-tools]

## <a name="open-the-sample-application"></a>Örnek uygulamayı Aç
Örnek uygulamayı açmak için şu adımları izleyin:

1. Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

`app.ino` Dosyasını `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın
Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:

1. Aygıtın aygıt bulma CLI ile seri bağlantı noktası alın:

   ```bash
   devdisco list --usb
   ```

   Usb Arduino panonuzu COM bağlantı noktasını bulun ve aşağıdakine benzer bir çıktı görmeniz gerekir: ![aygıt bulma][device-discovery]

2. Dosyayı açmak `config.json` Ders klasöründe bulunan COM bağlantı noktası numarası değerini ekleyin:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > COM bağlantı noktası, Windows platformunda için biçimi olan `COM1, COM2, ...`. MacOS veya Ubuntu, ile başlayan `/dev/`.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
### <a name="install-the-required-tools-for-your-arduino-board"></a>Arduino panonuz için gerekli Araçları'nı yükleme

Aşağıdaki komutu çalıştırarak Arduino panonuz için Azure IOT Hub SDK'sını yükleyin:

```bash
gulp install-tools
```

Bu görev, ağ bağlantınızın bağlı olarak tamamlanması uzun zaman alabilir.

> [!NOTE]
> Lütfen çalışan Arduino IDE örneği gulp görevleri çalıştırılırken çıkın: `install-tools`, `run`.

### <a name="deploy-and-run-the-sample-app"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a>Uygulama çalıştığını doğrulama
IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting-page] yaygın sorunların çözümleri için.

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a>Özet
Arduino panonuzu ile çalışmak için gerekli araçları yüklü ve ışığı yanıp sönen bir örnek uygulamanın Arduino panonuz için dağıtılır. Şimdi oluşturmanıza, dağıtmanıza ve Arduino panonuzu ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Araçları edinin][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md