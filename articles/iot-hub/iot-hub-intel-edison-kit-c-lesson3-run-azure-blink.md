---
title: "Azure IOT - Ders 3 Connect Intel Edison (C): ileti gönderme | Microsoft Docs"
description: "Dağıtma ve IOT hub'ına iletileri gönderir ve ışığı yanıp Intel Edison'u bir örnek uygulamayı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti arduino bulut için veri gönderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın
## <a name="what-you-will-do"></a>Ne yapacağını
Bu makalede, dağıtmak ve bir örnek uygulamanın IOT hub'ına iletileri gönderir Intel Edison'u çalıştırmak nasıl yapacağınızı gösterir. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Gulp aracı dağıtmak ve örnek C uygulama Edison'u üzerinde çalıştırmak için nasıl kullanılacağını öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
* Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir depolama hesabı oluştur][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma
Cihaz bağlantı dizesi Edison'u IOT hub'ınıza bağlanmak için kullanılır. IOT hub bağlantı dizesine Edison'u IOT hub'ı temsil eden cihaz kimliği IOT hub'ınıza bağlanmak için kullanılır.

* Kaynak grubunuzdaki tüm IOT hub aşağıdaki Azure CLI komutu çalıştırarak listesi:

```bash
az iot hub list -g iot-sample --query [].name
```

Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.

* IOT hub bağlantı dizesine aşağıdaki Azure CLI komutu çalıştırarak alın:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Edison'u kayıtlı belirtilen adıdır.

* Cihaz bağlantı dizesi, aşağıdaki komutu çalıştırarak alın:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Kullanım `myinteledison` değeri olarak `{device id}` değeri değiştirirseniz alamadık.

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın
1. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.

2. Aygıt yapılandırma dosyasını açın `config-edison.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. İçinde aşağıdaki değişiklikleri yapın `config-edison.json` dosyası:

   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında aygıt IP adresine sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** ile `device connection string` , elde edilen.
   * Değiştir **[IOT hub bağlantı dizesine]** ile `iot hub connection string` , elde edilen.

   > [!NOTE]
   > Gerekmeyen `azure_storage_connection_string` bu makalede. Olduğu gibi tutun.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak Edison'u üzerinde örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Örnek uygulama çalıştığını doğrulayın
Her iki saniye yanıp sönen Edison'u için bağlı LED görmeniz gerekir. IŞIĞI yanıp her zaman, örnek uygulamayı IOT hub'ınıza ileti gönderir ve iletinin IOT hub'ınıza başarıyla gönderildi doğrular. Ayrıca, IOT hub tarafından alınan her ileti konsol penceresinde yazdırılır. Örnek uygulama, 20 ileti gönderdikten sonra otomatik olarak sona erer.

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Özet
Dağıtılan artık ve IOT hub'ına cihaz bulut iletilerini göndermek için Edison'u yeni blink örnek uygulamayı çalıştırın. Depolama hesabına yazılan gibi şimdi iletilerinizi izleyin.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md