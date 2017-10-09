---
title: 'Connect Raspberry pi (C) tooAzure IOT - Ders 4: Bulut cihaz | Microsoft Docs'
description: "Örnek bir uygulama Pi üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri tooPi, IOT hub tooblink hello LED gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toodevice bulut, buluttan ileti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın
Bu makalede, Raspberry Pi 3 örnek bir uygulamayı dağıtın. Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler. Ayrıca bir gulp görev, bilgisayar toosend iletileri tooPi IOT hub'ından çalıştırın. Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-do"></a>Ne yapacağını
* Merhaba örnek uygulama tooyour IOT hub bağlayın.
* Dağıtma ve hello örnek uygulamayı çalıştırın.
* İletiler, IOT hub tooPi tooblink hello LED gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl IOT hub'ından toomonitor gelen iletileri.
* Nasıl toosend bulut-cihaz, IOT hub tooPi iletileri.

## <a name="what-you-need"></a>Ne gerekiyor
* Böğürtlenli Pi 3 ayarlamak için kullanın. Pi yukarı tooset nasıl görürüm toolearn [Cihazınızı yapılandırmak](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. toolearn nasıl toocreate IOT hub'ınızı bkz [IOT hub'ınızı oluşturma ve Raspberry Pi 3 kaydetme](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Merhaba örnek uygulama tooyour IOT hub'ı Bağlan
1. Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-raspberrypi-getting-started`. Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:

   ```bash
   cd Lesson4
   code .
   ```

   Bildirim hello `app.c` hello dosyasında `app` alt klasörü. Merhaba `app.c` hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası bir dosyadır. Merhaba `blinkLED` işlevi yanıp hello LED.

   ![Depodaki yapısında Merhaba örnek uygulaması](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```

   Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) dağıtma ve çalıştırmanın Merhaba örnek uygulaması toostep toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınır. Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-raspberrypi.json` dosya. Merhaba `config-raspberrypi.json` giriş klasörü hello alt klasöründe bir dosyadır.

   ![Merhaba config raspberrypi.json dosyasının içeriği](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** hello çalıştırarak aldığınız Pı'nin IP adresi veya ana bilgisayar adı ile `devdisco list --eth` komutu.
* Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` komutu.
* Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` komutu.

> [!NOTE]
> Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutları çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:

```
gulp deploy && gulp run
```

Merhaba gulp komutu çalıştırır yükleme araçları görev ilk hello. Ardından hello örnek uygulama tooPi dağıtır. Son olarak, bu Merhaba uygulaması Pi ve ayrı bir görev, ana bilgisayardaki bilgisayar toosend 20 blink iletileri tooPi IOT hub'ından çalışır.

Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır. Bu sırada, hello gulp görev, IOT hub tooPi birkaç "blink" iletileri gönderir. Pi alan her blink ileti için hello örnek uygulama çağırır hello `blinkLED` işlevi tooblink hello LED.

Görev gönderir 20 iletilerden IOT hub tooPi gulp hello LED blink her iki saniye hello olarak görmeniz gerekir. Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.

![Örnek uygulama ile komut gulp ve iletileri blink](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a>Özet
İleti, IOT hub tooPi tooblink hello LED başarıyla gönderdik. Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba açma ve kapatma hello LED davranışını değiştirme](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
