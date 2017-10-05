---
title: "Azure IOT - Ders 4 Intel Edison'u (düğüm) bağlanma: iletileri alacak | Microsoft Docs"
description: "Örnek bir uygulama Edison'u üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri için Edison'u LED blink için IOT hub'gönderir."
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
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın
Bu makalede, Intel Edison'u üzerinde örnek bir uygulamayı dağıtın. Örnek uygulama IOT hub'ınızı gelen iletilere izler. Ayrıca Edison'u için IOT hub'ından iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın. Örnek uygulama iletileri aldığında ışığı yanıp. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-do"></a>Ne yapacağını
* Örnek uygulama IOT hub'ınıza bağlanın.
* Dağıtma ve örnek uygulamayı çalıştırın.
* İletileri LED blink Edison'u için IOT hub'ından gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* IOT hub'ınızı gelen iletilere izlemek nasıl.
* Edison'u için IOT hub'ından bulut-cihaz iletilerini göndermek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor
* Intel Edison'u ayarlamak için kullanın. Edison'u ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak][configure-your-device].
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. IOT hub'ınızı oluşturmayı öğrenmek için bkz: [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Örnek uygulama IOT hub'ınıza bağlanın
1. Depodaki klasöründe olduğunuzdan emin olun `iot-hub-node-edison-getting-started`. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

   ```bash
   cd Lesson4
   code .
   ```

   Dosyada `app` alt IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası klasörüdür. `blinkLED` İşlevi yanıp LED.

   ![Depodaki yapısında örnek uygulama][repo-structure]
2. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```

   ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma ve örnek uygulama çalıştırılıyor görev adımı atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır. ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] yer tutucuları değiştirmek gereken başka bir bilgisayara `config-edison.json` dosya. `config-edison.json` Giriş klasörü alt klasöründe bir dosyadır.

   ![Config edison.json dosyasının içeriği](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında aygıt IP adresine sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.
   * Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutları çalıştırarak Edison'u üzerinde örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

Gulp komutu Edison'u örnek uygulamayı dağıtır. Ardından, IOT hub'ından Edison'u için 20 blink iletileri göndermek için Edison'u ve ana bilgisayarınızda ayrı bir görev uygulama çalışır.

Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır. Bu sırada, gulp görev Edison'u için IOT hub'ından birkaç "blink" iletileri gönderir. Örnek uygulama Edison'u alan her blink ileti için çağırır `blinkLED` LED blink işlevi.

Gulp görev 20 iletileri IOT hub'ından için Edison'u gönderir, her iki saniye LED blink görmeniz gerekir. Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.

![Örnek uygulama ile komut gulp ve iletileri blink][gulp-command-and-blink-messages]

## <a name="summary"></a>Özet
IOT hub'ından LED blink Edison'u için başarıyla iletileri gönderdik. Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Açık ve kapalı LED davranışını değiştirme][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md