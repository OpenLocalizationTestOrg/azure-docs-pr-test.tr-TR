---
title: "Azure IOT - Ders 3 Raspberry Pi'yi (düğüm) bağlanma: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve IOT hub'ına iletileri gönderir ve ışığı yanıp Raspberry Pi 3 örnek uygulamayı çalıştırın."
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
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın
## <a name="what-you-will-do"></a>Ne yapacağını
Bu makalede dağıtmak ve IOT hub'ına iletileri gönderir Raspberry Pi 3 örnek bir uygulamayı çalıştırmak nasıl yapacağınızı gösterir. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Gulp aracı dağıtmak ve örnek Node.js uygulaması Pi üzerinde çalıştırmak için nasıl kullanılacağını öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
* Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir depolama hesabı oluştur](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IOT hub ve cihaz bağlantı dizeleri alma
Cihaz bağlantı dizesi, Pi tarafından IOT hub'ınıza bağlanmak için kullanılır. IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır. 

* Kaynak grubunuzdaki tüm IOT hub aşağıdaki Azure CLI komutu çalıştırarak listesi:

```bash
az iot hub list -g iot-sample --query [].name
```

Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.

* IOT hub bağlantı dizesine aşağıdaki Azure CLI komutu çalıştırarak alın:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Pi kayıtlı belirtilen adıdır.

* Cihaz bağlantı dizesi, aşağıdaki komutu çalıştırarak alın:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Kullanım `myraspberrypi` değeri olarak `{device id}` değeri değiştirirseniz alamadık.

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın
1. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:
   
   ```bash
   npm install
   gulp init
   ```
2. Aygıt yapılandırma dosyasını açın `config-raspberrypi.json` aşağıdaki komutu çalıştırarak Visual Studio Code:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. İçinde aşağıdaki değişiklikleri yapın `config-raspberrypi.json` dosyası:
   
   * Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** dan aldığınız cihaz IP adresi veya ana bilgisayar adı ile `device-discovery-cli` veya Cihazınızı yapılandırıldığında devralınan değere sahip.
   * Değiştir **[IOT cihaz bağlantı dizesi]** ile `device connection string` , elde edilen.
   * Değiştir **[IOT hub bağlantı dizesine]** ile `iot hub connection string` , elde edilen.

Güncelleştirme `config-raspberrypi.json` bilgisayarınızdan örnek uygulama dağıtabilirsiniz, böylece dosya.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Örnek uygulama çalıştığını doğrulayın
Her iki saniye yanıp sönen Pi bağlı LED görmeniz gerekir. IŞIĞI yanıp her zaman, örnek uygulamayı IOT hub'ınıza ileti gönderir ve iletinin IOT hub'ınıza başarıyla gönderildi doğrular. Ayrıca, IOT hub tarafından alınan her ileti konsol penceresinde yazdırılır. Örnek uygulama, 20 ileti gönderdikten sonra otomatik olarak sona erer.

![Örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Özet
Dağıtılan artık ve IOT hub'ına cihaz bulut iletilerini göndermek için Pi üzerinde yeni blink örnek uygulamayı çalıştırın. Depolama hesabına yazılan gibi iletilerinizi şimdi izleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

