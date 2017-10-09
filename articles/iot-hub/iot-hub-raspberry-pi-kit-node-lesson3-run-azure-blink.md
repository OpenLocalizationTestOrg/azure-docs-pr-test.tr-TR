---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooRaspberry tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp Pi 3 çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: blink bulut pi neden, buluttan blink neden
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Örnek uygulama toosend cihaz bulut iletilerini çalıştırın
## <a name="what-you-will-do"></a>Ne yapacağını
Bu makale size nasıl toodeploy ve gönderir Raspberry Pi 3 örnek bir uygulama çalıştırılmasında iletileri tooyour IOT hub'ı gösterir. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Nasıl toouse hello aracı toodeploy gulp ve Merhaba örnek Node.js uygulaması Pi üzerinde çalıştırmak öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
* Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma
Merhaba cihaz bağlantı dizesi, Pi tooconnect tooyour IOT hub tarafından kullanılır. Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir. 

* Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:

```bash
az iot hub list -g iot-sample --query [].name
```

Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.

* Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Pi kayıtlı belirtilen hello adıdır.

* Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Kullanım `myraspberrypi` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:
   
   ```bash
   npm install
   gulp init
   ```
2. Açık hello aygıt yapılandırma dosyası `config-raspberrypi.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Merhaba değişikliklerini aşağıdaki hello olun `config-raspberrypi.json` dosyası:
   
   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** dan aldığınız hello aygıt IP adresi veya ana bilgisayar adı ile `device-discovery-cli` veya Cihazınızı yapılandırıldığında devralınan hello değerine sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.
   * Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.

Güncelleştirme hello `config-raspberrypi.json` Merhaba örnek uygulaması bilgisayarınızdan dağıtabilirsiniz dosyasını.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Merhaba örnek uygulaması çalıştığını doğrulayın
Her iki saniye yanıp sönen bağlı tooPi olan hello LED görmeniz gerekir. Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular. Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır. Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.

![Örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Özet
Dağıtılan artık ve Pi toosend cihaz bulut iletilerini tooyour IOT hub'ına hello yeni blink örnek uygulamayı çalıştırın. Toohello depolama hesabı yazıldığı şekilde iletilerinizi şimdi izleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

