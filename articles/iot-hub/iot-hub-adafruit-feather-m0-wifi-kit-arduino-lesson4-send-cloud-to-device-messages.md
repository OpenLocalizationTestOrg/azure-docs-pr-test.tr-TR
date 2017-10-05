---
title: "Azure IOT - Ders 4 Arduino (C) bağlanın: Bulut cihaz | Microsoft Docs"
description: "Örnek bir uygulama Adafruit yumuşatma M0 WiFi ve izleyiciler gelen iletileri IOT hub'ından çalışır. Yeni bir gulp görev, IOT hub ' LED blink Adafruit yumuşatma M0 WiFi iletileri gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Web, web üzerinden öncülük arduino denetim neden arduino denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın
Bu makaledeki örnek bir uygulama Adafruit yumuşatma M0 WiFi Arduino Panonuzda dağıtın.

Örnek uygulama IOT hub'ınızı gelen iletilere izler. Ayrıca, IOT hub'ından Arduino panonuzu iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın. Örnek uygulama iletileri aldığında ışığı yanıp. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-do"></a>Ne yapacağını
* Örnek uygulama IOT hub'ınıza bağlanın.
* Dağıtma ve örnek uygulamayı çalıştırın.
* İletileri IOT hub'ından LED blink için Arduino panonuzu gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* IOT hub'ınızı gelen iletilere izlemek nasıl.
* Bulut cihaz IOT hub'ından Arduino panonuzu göndermek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor
* Arduino panonuzu ayarlamak için kullanın. Arduino panonuzu ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak][configure-your-device].
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. IOT hub'ınızı oluşturmayı öğrenmek için bkz: [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Örnek uygulama IOT hub'ınıza bağlanın

1. Depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-feather-m0-getting-started`.

   Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

   ```bash
   cd Lesson4
   code .
   ```

   Bildirim `app.ino` dosyasını `app` alt klasörü. `app.ino` IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası bir dosyadır. `blinkLED` İşlevi yanıp LED.

   ![Depodaki yapısında örnek uygulama][repo-structure]

2. Aygıtın aygıt bulma CLI ile seri bağlantı noktası alın:

   ```bash
   devdisco list --usb
   ```

   Aşağıdakine benzer bir çıktı görmeniz ve usb Arduino panonuzu COM bağlantı noktasını Bul:

   ![Aygıt Bulma][device-discovery]

3. Dosyayı açmak `config.json` Ders klasöründe ve giriş bulunan COM bağlantı noktası numarası değeri:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > COM bağlantı noktası, Windows platformunda için biçimi olan `COM1, COM2, ...`. MacOS veya Ubuntu, ile başlar `/dev/`.

4. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. İçinde aşağıdaki değişiklikleri yapın `config-arduino.json` dosyası:

   ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma ve örnek uygulama çalıştırılıyor görev adımı atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır. ' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] yer tutucuları değiştirmek gereken başka bir bilgisayara `config-arduino.json` dosya. `config-arduino.json` Giriş klasörü alt klasöründe bir dosyadır.

   ![Config arduino.json dosyasının içeriği][config-arduino-json]

   * Değiştir **[Wi-Fi SSID]** Internet'e bağlı, Wi-Fi SSID ile.
   * Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla. Wi-Fi parola gerektirmez, dize kaldırın.
   * Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.
   * Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutları çalıştırarak Arduino Panonuzda örnek uygulamayı çalıştırın:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Gulp komutu Arduino panonuzu örnek uygulamayı dağıtır. Ardından, Arduino panonuzu ve ana bilgisayarınızda IOT hub'ından Arduino panonuzu 20 blink iletileri göndermek için ayrı bir görev uygulama çalışır.

Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır. Bu sırada, gulp görev Arduino panonuzu IOT hub'ından birkaç "blink" iletileri gönderir. Pano alan her blink ileti için örnek uygulama çağırır `blinkLED` LED blink işlevi.

Gulp görev 20 iletileri IOT hub'ından Arduino panonuzu gönderir, her iki saniye LED blink görmeniz gerekir. Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.

![Örnek uygulama ile komut gulp ve iletileri blink][sample-application]

## <a name="summary"></a>Özet
IOT hub'ından LED blink için Arduino panonuz başarıyla iletileri gönderdik. Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Açık ve kapalı LED davranışını değiştirme][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md