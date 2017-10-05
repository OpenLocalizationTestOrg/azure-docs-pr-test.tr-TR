---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: uygulama dağıtma | Microsoft Docs"
description: "Örnek C uygulama github'dan kopyalama ve Intel Edison'u panonuzu bu uygulamayı dağıtmak için gulp çalıştırın. Bu örnek uygulama panosuna her iki saniye bağlı ışığı yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projeleri arduino neden, arduino öncülük blink, neden arduino blink kodunu arduino blink programı, arduino blink örneği"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Blink uygulaması oluşturma ve dağıtma
## <a name="what-you-will-do"></a>Ne yapacağını
Örnek C uygulama github'dan kopyalama ve Intel Edison'u örnek uygulamayı dağıtmak için gulp aracını kullanın. Örnek uygulama panosuna her iki saniye bağlı ışığı yanıp. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
* Nasıl dağıtmak ve Edison'u üzerinde örnek uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor
Aşağıdaki işlemleri başarıyla tamamlandı gerekir:

* [Cihazınızı yapılandırın][configure-your-device]
* [Araçları edinin][get-the-tools]

## <a name="open-the-sample-application"></a>Örnek uygulamayı Aç
Örnek uygulamayı açmak için şu adımları izleyin:

1. Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

Dosyada `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın
Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:

1. Aşağıdaki komutu çalıştırarak aygıt yapılandırma dosyası oluşturun:

   ```bash
   gulp init
   ```

   Yapılandırma dosyası `config-edison.json` Edison'u için oturum açmak için kullandığınız kullanıcı kimlik bilgilerini içerir. Kullanıcı kimlik bilgilerini sızıntısını önlemek için yapılandırma dosyası alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda giriş klasörünün.

2. Aygıt yapılandırma dosyası, aşağıdaki komutu çalıştırarak Visual Studio kodda açın:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Yer tutucu Değiştir `[device hostname or IP address]` ve `[device password]` içinde önceki Ders düşürüleceği parolanın ve IP adresi ile.

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Tebrikler! İlk örnek uygulama Edison'u için başarıyla oluşturdunuz.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma

### <a name="deploy-and-run-the-sample-app"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Uygulama çalıştığını doğrulama
Örnek uygulama için 20 kez ışığı yanıp sonra otomatik olarak sonlandırır. IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a>Özet
Edison'u ile çalışmak için gerekli araçları yüklü ve ışığı yanıp sönen bir örnek uygulamanın Edison'u için dağıtılır. Şimdi oluşturmanıza, dağıtmanıza ve Edison'u ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Araçları edinin][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
