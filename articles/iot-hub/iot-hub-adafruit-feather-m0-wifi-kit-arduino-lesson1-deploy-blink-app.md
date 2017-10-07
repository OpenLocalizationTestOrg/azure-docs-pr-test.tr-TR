---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek Arduino uygulaması github'dan kopyalayın ve bu uygulama tooyour Adafruit yumuşatma M0 WiFi gulp toodeploy çalıştırın. Bu örnek uygulama hello GPIO'yu yanıp"
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
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Merhaba blink uygulama oluşturun ve dağıtın
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba örnek Arduino uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooyour Adafruit yumuşatma M0 WiFi Arduino Panosu kullanın. Merhaba örnek uygulama yanıp sönme hello barod GPIO'yu #13 her iki saniye GEREKTİRİYORDU.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting-page].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
* Nasıl toodeploy ve çalışma hello Arduino panonuzu üzerinde örnek uygulama.

## <a name="what-you-need"></a>Ne gerekiyor
Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:

* [Cihazınızı yapılandırın][configure-your-device]
* [Merhaba araçları edinin][get-the-tools]

## <a name="open-hello-sample-application"></a>Açık Merhaba örnek uygulaması
tooopen hello örnek uygulama, aşağıdaki adımları izleyin:

1. Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

Merhaba `app.ino` hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:

1. Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:

   ```bash
   devdisco list --usb
   ```

   Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul: ![aygıt bulma][device-discovery]

2. Açık hello dosya `config.json` hello Ders klasörü ve COM bağlantı noktası numarası bulunan hello hello değerini ekleyin:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`. MacOS veya Ubuntu, ile başlayan `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Arduino panonuz için gerekli hello araçlarını yükleme

Hello Azure IOT Hub SDK'sı Arduino panonuz için komutu aşağıdaki hello çalıştırarak yükleyin:

```bash
gulp install-tools
```

Bu görev, ağ bağlantınızın bağlı olarak bir uzun süre toocomplete alabilir.

> [!NOTE]
> Lütfen gulp görevler çalışırken Arduino IDE örneği hello çıkın: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Merhaba uygulama çalıştığını doğrulama
Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting-page] çözümleri toocommon sorunları.

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a>Özet
Gerekli hello araçları toowork Arduino panonuzu yüklü ve bir örnek uygulama tooyour Arduino Panosu tooblink hello LED dağıtılır. Artık oluşturmak, dağıtmak ve Arduino Panosu tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alacak.

## <a name="next-steps"></a>Sonraki adımlar
[Hello Azure Araçları edinin][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md