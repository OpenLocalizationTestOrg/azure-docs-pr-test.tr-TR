---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 1: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek C uygulaması github'dan kopyalayın ve bu uygulama tooyour Intel Edison'u Panosu gulp toodeploy çalıştırın. Bu örnek uygulama hello bağlı LED toohello Panosu her iki saniye yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projeleri arduino neden, arduino öncülük blink, neden arduino blink kodunu arduino blink programı, arduino blink örneği"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Merhaba blink uygulama oluşturun ve dağıtın
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba örnek C uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooIntel Edison'u kullanın. Merhaba örnek uygulaması, her iki saniye hello bağlı LED toohello Panosu yanıp. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
* Nasıl toodeploy ve çalışma hello Edison'u üzerinde örnek uygulama.

## <a name="what-you-need"></a>Ne gerekiyor
Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:

* [Cihazınızı yapılandırın][configure-your-device]
* [Merhaba araçları edinin][get-the-tools]

## <a name="open-hello-sample-application"></a>Açık Merhaba örnek uygulaması
tooopen hello örnek uygulama, aşağıdaki adımları izleyin:

1. Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

Merhaba Hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:

1. Hello aşağıdaki komutu çalıştırarak Hello aygıt yapılandırma dosyası oluşturun:

   ```bash
   gulp init
   ```

   Merhaba yapılandırma dosyası `config-edison.json` içinde tooEdison toolog kullanmak hello kullanıcı kimlik bilgilerini içerir. tooavoid hello sızıntısı kullanıcı kimlik bilgilerini, hello yapılandırma dosyası hello alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda hello giriş klasörünün.

2. Merhaba aygıt yapılandırma dosyasını Visual Studio kodda hello aşağıdaki komutu çalıştırarak açın:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Merhaba yer tutucu Değiştir `[device hostname or IP address]` ve `[device password]` başlangıç IP adresi ve içinde önceki Ders düşürüleceği parola.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Tebrikler! Merhaba ilk örnek bir uygulama için Edison'u başarıyla oluşturdunuz.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a>Üzerinde Edison'u Hello Azure IOT Hub SDK'sını yükleyin
Hello Azure IOT Hub SDK'sı üzerinde Edison'u hello aşağıdaki komutu çalıştırarak yükleyin:

```bash
gulp install-tools
```

Bu görev, ağ bağlantınızın bağlı olarak bir uzun süre toocomplete alabilir. Bunun ihtiyaçlarını toobe çalışması yalnızca bir kez bir Edison'u için.

### <a name="deploy-and-run-hello-sample-app"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Merhaba uygulama çalıştığını doğrulama
Merhaba örnek uygulama için 20 kez Hello ışığı yanıp sonra otomatik olarak sonlandırır. Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a>Özet
Gerekli hello araçları toowork ile Edison'u yüklü ve örnek uygulama tooEdison tooblink hello LED dağıtılır. Artık oluşturmak, dağıtmak ve Edison'u tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Hello Azure Araçları edinin][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
