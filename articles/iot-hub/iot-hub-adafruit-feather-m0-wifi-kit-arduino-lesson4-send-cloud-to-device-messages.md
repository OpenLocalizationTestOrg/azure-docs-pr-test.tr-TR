---
title: 'Connect Arduino (C) tooAzure IOT - Ders 4: Bulut cihaz | Microsoft Docs'
description: "Örnek bir uygulama Adafruit yumuşatma M0 WiFi ve izleyiciler gelen iletileri IOT hub'ından çalışır. Yeni bir gulp görevi, IOT hub tooblink hello LED iletileri tooAdafruit yumuşatma M0 WiFi gönderir."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın
Bu makaledeki örnek bir uygulama Adafruit yumuşatma M0 WiFi Arduino Panonuzda dağıtın.

Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler. Ayrıca bir gulp görev, bilgisayar toosend iletileri tooyour Arduino Panosu üzerinde IOT hub'ından çalıştırın. Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-do"></a>Ne yapacağını
* Merhaba örnek uygulama tooyour IOT hub bağlayın.
* Dağıtma ve hello örnek uygulamayı çalıştırın.
* İletiler, IOT hub tooyour Arduino Panosu tooblink hello LED gönderin.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl IOT hub'ından toomonitor gelen iletileri.
* Nasıl toosend bulut-cihaz IOT hub tooyour Arduino Panosu iletileri.

## <a name="what-you-need"></a>Ne gerekiyor
* Arduino panonuzu ayarlamak için kullanın. tooset Arduino panonuzu yukarı nasıl görürüm toolearn [Cihazınızı yapılandırmak][configure-your-device].
* Azure aboneliğinizde oluşturduğunuz IOT hub'ı. toolearn nasıl toocreate IOT hub'ınızı bkz [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Merhaba örnek uygulama tooyour IOT hub'ı Bağlan

1. Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-feather-m0-getting-started`.

   Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:

   ```bash
   cd Lesson4
   code .
   ```

   Bildirim hello `app.ino` hello dosyasında `app` alt klasörü. Merhaba `app.ino` hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası bir dosyadır. Merhaba `blinkLED` işlevi yanıp hello LED.

   ![Depodaki yapısında Merhaba örnek uygulaması][repo-structure]

2. Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:

   ```bash
   devdisco list --usb
   ```

   Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul:

   ![Aygıt Bulma][device-discovery]

3. Açık hello dosya `config.json` hello Ders klasöründe ve COM bağlantı noktası numarası bulunan hello giriş hello değeri:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`. MacOS veya Ubuntu, ile başlar `/dev/`.

4. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Merhaba değişikliklerini aşağıdaki hello olun `config-arduino.json` dosyası:

   Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma hello adım toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınan ve Merhaba örnek uygulama çalıştırılıyor. Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-arduino.json` dosya. Merhaba `config-arduino.json` giriş klasörü hello alt klasöründe bir dosyadır.

   ![Merhaba config arduino.json dosyasının içeriği][config-arduino-json]

   * Değiştir **[Wi-Fi SSID]** toohello Internet bağlı, Wi-Fi SSID ile.
   * Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla. Wi-Fi parola gerektirmez, hello dize kaldırın.
   * Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.
   * Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutları çalıştırarak Arduino Panonuzda hello örnek uygulamayı çalıştırın:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Merhaba gulp komutu hello örnek uygulama tooyour Arduino Panosu dağıtır. Ardından, onu Merhaba uygulaması Arduino panonuzu ve ana bilgisayarınızda ayrı bir görev bilgisayar toosend 20 blink iletileri tooyour Arduino Panosu IOT hub'ından çalışır.

Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır. Bu sırada, hello gulp görev, IOT hub tooyour Arduino Panosu birkaç "blink" iletileri gönderir. Pano hello her blink iletiyi alır için hello örnek uygulama hello çağırır `blinkLED` işlevi tooblink hello LED.

Merhaba LED görmelisiniz hello gulp görev, IOT hub tooyour Arduino Panosu 20 ileti gönderir gibi her iki saniye blink. Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.

![Örnek uygulama ile komut gulp ve iletileri blink][sample-application]

## <a name="summary"></a>Özet
İleti, IOT hub tooyour Arduino Panosu tooblink hello LED başarıyla gönderdik. Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba açma ve kapatma hello LED davranışını değiştirme][change-the-on-and-off-led-behavior]


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