---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 4 bağlanın: iletileri alacak | Microsoft Docs"
description: "Örnek bir uygulama Edison'u üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri tooEdison, IOT hub tooblink hello LED gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Web, web üzerinden öncülük arduino denetim neden arduino denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın
Bu makalede, Intel Edison'u üzerinde örnek bir uygulamayı dağıtın. Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler. Ayrıca bir gulp görev, bilgisayar toosend iletileri tooEdison IOT hub'ından çalıştırın. Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-do"></a>Ne yapacağını
* Merhaba örnek uygulama tooyour IOT hub bağlayın.
* Dağıtma ve hello örnek uygulamayı çalıştırın.
* İletiler, IOT hub tooEdison tooblink hello LED gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl IOT hub'ından toomonitor gelen iletileri.
* Nasıl toosend bulut-cihaz, IOT hub tooEdison iletileri.

## <a name="what-you-need"></a>Ne gerekiyor
* Intel Edison'u ayarlamak için kullanın. tooset Edison'u, Yukarı nasıl görürüm toolearn [Cihazınızı yapılandırmak][configure-your-device].
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. toolearn nasıl toocreate IOT hub'ınızı bkz [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Merhaba örnek uygulama tooyour IOT hub'ı Bağlan
1. Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-node-edison-getting-started`. Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:

   ```bash
   cd Lesson4
   code .
   ```

   Merhaba Hello dosyasında `app` alt hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası klasörüdür. Merhaba `blinkLED` işlevi yanıp hello LED.

   ![Depodaki yapısında Merhaba örnek uygulaması][repo-structure]
2. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```

   Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma hello adım toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınan ve Merhaba örnek uygulama çalıştırılıyor. Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-edison.json` dosya. Merhaba `config-edison.json` giriş klasörü hello alt klasöründe bir dosyadır.

   ![Merhaba config edison.json dosyasının içeriği](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında hello cihaz IP adresine sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.
   * Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutları çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

Merhaba gulp komutu hello örnek uygulama tooEdison dağıtır. Ardından, onu Merhaba uygulaması Edison'u ve ana bilgisayarınızda ayrı bir görev bilgisayar toosend 20 blink iletileri tooEdison IOT hub'ından çalışır.

Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır. Bu sırada, hello gulp görev, IOT hub tooEdison birkaç "blink" iletileri gönderir. Edison'u alan her blink ileti için hello örnek uygulama çağırır hello `blinkLED` işlevi tooblink hello LED.

Görev gönderir 20 iletilerden IOT hub tooEdison gulp hello LED blink her iki saniye hello olarak görmeniz gerekir. Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.

![Örnek uygulama ile komut gulp ve iletileri blink][gulp-command-and-blink-messages]

## <a name="summary"></a>Özet
İleti, IOT hub tooEdison tooblink hello LED başarıyla gönderdik. Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba açma ve kapatma hello LED davranışını değiştirme][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md