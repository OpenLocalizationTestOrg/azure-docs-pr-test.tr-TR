---
title: "Connect Arduino (C) tooAzure IOT - Ders 3: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooAdafruit tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp yumuşatma M0 WiFi çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti, arduino veri toocloud Gönder"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Örnek uygulama toosend cihaz bulut iletilerini çalıştırın
## <a name="what-you-will-do"></a>Ne yapacağını
Bu makale toodeploy ve Adafruit yumuşatma M0 WiFi Arduino örnek bir uygulama çalıştırılmasında bu gönderdiği iletileri tooyour IOT hub'ın nasıl tahtası gösterir.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Nasıl toouse hello aracı toodeploy gulp ve Arduino Panonuzda hello örnek Arduino uygulamayı çalıştırın öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
* Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma
Merhaba cihaz bağlantı dizesi kullanılan tooconnect Arduino Panosu tooyour IOT hub'ınızın olan. Merhaba IOT hub bağlantı dizesine kullanılan tooconnect, Arduino temsil eden IOT hub toohello cihaz kimliğinizi tahtası hello IOT hub ' dir.

* Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:

```bash
az iot hub list -g iot-sample --query [].name
```

Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.

* Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`IOT hub'ınızı oluşturduğunuzda ve Arduino panonuzu kayıtlı belirttiğiniz hello adıdır.

* Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Kullanım `mym0wifi` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.
## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:

1. Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:

   ```bash
   devdisco list --usb
   ```

   Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul:

   ![Aygıt Bulma][device-discovery]

2. Açık hello dosya `config.json` hello Ders klasörü ve COM bağlantı noktası numarası bulunan hello hello değerini ekleyin:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`. MacOS veya Ubuntu, ile başlayan `/dev/`.

3. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Açık hello aygıt yapılandırma dosyası `config-arduino.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. Merhaba değişikliklerini aşağıdaki hello olun `config-arduino.json` dosyası:

   * Değiştir **[Wi-Fi SSID]** toohello Internet bağlı, Wi-Fi SSID ile.
   * Değiştir **[Wi-Fi parola]** Wi-Fi parolanızla. Wi-Fi parola gerektirmez, hello dize kaldırın.
   * Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.
   * Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.

   > [!NOTE]
   > Gerekmeyen `azure_storage_connection_string` bu makalede. Olduğu gibi tutun.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak Arduino Panonuzda hello örnek uygulamayı çalıştırın:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Merhaba varsayılan gulp görev çalıştırır `install-tools` ve `run` sırayla görevler. Olduğunda, [hello blink uygulama][deployed-the-blink-app], bu görevleri ayrı ayrı çalıştı.

## <a name="verify-that-hello-sample-application-works"></a>Merhaba örnek uygulaması çalıştığını doğrulayın
Merhaba GPIO'yu #0 yerleşik LED her iki saniye yanıp sönen görmeniz gerekir. Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular. Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır. Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Özet
Dağıtılan artık ve Arduino Panosu toosend cihaz bulut iletilerini tooyour IOT hub'ınızı üzerinde hello yeni blink örnek uygulamayı çalıştırın. Toohello depolama hesabı yazıldığı şekilde şimdi iletilerinizi izleyin.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md