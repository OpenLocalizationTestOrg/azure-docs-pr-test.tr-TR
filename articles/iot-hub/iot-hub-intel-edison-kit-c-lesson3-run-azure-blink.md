---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 3: ileti gönderme | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooIntel tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp Edison'u çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti, arduino veri toocloud Gönder"
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
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Örnek uygulama toosend cihaz bulut iletilerini çalıştırın
## <a name="what-you-will-do"></a>Ne yapacağını
Bu makale size nasıl toodeploy ve gönderir Intel Edison'u örnek bir uygulama çalıştırılmasında iletileri tooyour IOT hub'ı gösterir. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Siz nasıl toouse hello gulp aracı toodeploy öğrenin ve üzerinde Edison'u hello örnek C uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor
* Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma
kullanılan tooconnect tooyour IOT hub'ı Edison'u Hello cihaz bağlantı dizesidir. IOT hub bağlantı dizesine hello kullanılan tooconnect Edison'u hello IOT hub'ı temsil eden, IOT hub toohello aygıt kimliğidir.

* Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:

```bash
az iot hub list -g iot-sample --query [].name
```

Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.

* Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Edison'u kayıtlı belirtilen hello adıdır.

* Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Kullanım `myinteledison` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.

2. Açık hello aygıt yapılandırma dosyası `config-edison.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Merhaba değişikliklerini aşağıdaki hello olun `config-edison.json` dosyası:

   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında hello cihaz IP adresine sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.
   * Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.

   > [!NOTE]
   > Gerekmeyen `azure_storage_connection_string` bu makalede. Olduğu gibi tutun.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Merhaba örnek uygulaması çalıştığını doğrulayın
Her iki saniye yanıp sönen bağlı tooEdison olan hello LED görmeniz gerekir. Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular. Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır. Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Özet
Dağıtılan artık ve hello yeni blink örnek uygulamayı Edison'u üzerinde toosend cihaz bulut iletilerini tooyour IOT hub'ı çalıştırın. Toohello depolama hesabı yazıldığı şekilde şimdi iletilerinizi izleyin.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md