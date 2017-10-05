---
title: "Azure IOT - Ders 4 Böğürtlenli Pi (C) bağlanın: Bulut cihaz | Microsoft Docs"
description: "Örnek bir uygulama Pi üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev, IOT hub ' LED blink Pi iletileri gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: cihaz, bulut iletiden bulut
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
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın
Bu makalede, Raspberry Pi 3 örnek bir uygulamayı dağıtın. Örnek uygulama IOT hub'ınızı gelen iletilere izler. Ayrıca, IOT hub'ından Pi iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın. Örnek uygulama iletileri aldığında ışığı yanıp. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-do"></a>Ne yapacağını
* Örnek uygulama IOT hub'ınıza bağlanın.
* Dağıtma ve örnek uygulamayı çalıştırın.
* İletileri LED blink Pi için IOT hub'ından gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* IOT hub'ınızı gelen iletilere izlemek nasıl.
* Pi IOT hub'ından bulut-cihaz iletilerini göndermek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor
* Böğürtlenli Pi 3 ayarlamak için kullanın. Pi ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. IOT hub'ınızı oluşturmayı öğrenmek için bkz: [IOT hub'ınızı oluşturma ve Raspberry Pi 3 kaydetme](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Örnek uygulama IOT hub'ınıza bağlanın
1. Depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-raspberrypi-getting-started`. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

   ```bash
   cd Lesson4
   code .
   ```

   Bildirim `app.c` dosyasını `app` alt klasörü. `app.c` IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası bir dosyadır. `blinkLED` İşlevi yanıp LED.

   ![Depodaki yapısında örnek uygulama](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```

   ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) dağıtma ve örnek uygulama çalıştırılıyor göreve adıma atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır. ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) yer tutucuları değiştirmek gereken başka bir bilgisayara `config-raspberrypi.json` dosya. `config-raspberrypi.json` Giriş klasörü alt klasöründe bir dosyadır.

   ![Config raspberrypi.json dosyasının içeriği](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** çalıştırarak aldığınız Pı'nin IP adresi veya ana bilgisayar adı ile `devdisco list --eth` komutu.
* Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` komutu.
* Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` komutu.

> [!NOTE]
> Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutları çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:

```
gulp deploy && gulp run
```

Gulp komutu ilk yükleme araçları görev çalıştırır. Ardından Pi örnek uygulamayı dağıtır. Son olarak, bu uygulama Pi ve ana bilgisayarınızda ayrı bir görev IOT hub'ından Pi 20 blink iletileri göndermeye çalışır.

Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır. Bu sırada, gulp görev birkaç "blink" Pi için IOT hub'ınızı gelen iletileri gönderir. Pi alan her blink ileti için örnek uygulama çağırır `blinkLED` LED blink işlevi.

Gulp görev 20 iletileri IOT hub'ından Pi gönderir, her iki saniye LED blink görmeniz gerekir. Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.

![Örnek uygulama ile komut gulp ve iletileri blink](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a>Özet
IOT hub'ından LED blink Pi için başarıyla iletileri gönderdik. Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Açık ve kapalı LED davranışını değiştirme](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
