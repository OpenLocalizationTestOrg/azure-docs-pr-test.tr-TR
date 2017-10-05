---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "BIRAK SensorTag ve IOT hub'ınızı ' ndan veri almaya bırak örnek uygulamayı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bırak uygulama, algılayıcı İzleyici uygulama, algılayıcı veri toplama, algılayıcılar, bulut için algılayıcı verilerini verileri"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Yapılandırma ve bırak örnek uygulamayı çalıştırma

## <a name="what-you-will-do"></a>Ne yapacağını

- Örnek depoyu kopyalayın. 
- SensorTag ve Intel NUC arasında bağlantı kurun. 
- IOT hub ve silinmesini devre dışı bırak (Bluetooth düşük enerji) örnek uygulaması SensorTag bilgilerini almak için Azure CLI kullanın. Yapılandırmak ve bırak örnek uygulamayı çalıştırın. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu makalede, şunları öğreneceksiniz:

- Nasıl yapılandırmak ve bırak örnek uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor

Başarılı bir şekilde tamamladınız gerekir

- [IOT hub'ı oluşturma ve SensorTag kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Ana bilgisayara örnek depoyu kopyalayın

Örnek deposuna kopyalamak için ana bilgisayarda aşağıdaki adımları izleyin:

1. Windows komut istemi penceresi açın veya terminal macOS veya Ubuntu açın.
2. Aşağıdaki komutları çalıştırın:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a>SensorTag ve Intel NUC arasında bağlantılar kurmak

Bağlantı kurmak için ana bilgisayarda aşağıdaki adımları izleyin:

1. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Açık `config-gateway.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Aşağıdaki kod satırını bulun ve değiştirin `[device hostname or IP address]` Intel NUC IP adresi veya ana bilgisayar adı.
   ![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Yardımcı Araçlar, aşağıdaki komutu çalıştırarak üzerinde Intel NUC yükleyin:

   ```bash
   gulp install-tools
   ```

5. Aşağıdaki resim olarak güç düğmesine basarak üzerinde SensorTag açın ve yeşil LED blink.

   ![Algılayıcı etiketi Aç](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Aşağıdaki komutları çalıştırarak SensorTag aygıtlarını tara:

   ```bash
   gulp discover-sensortag
   ```

7. Aşağıdaki komutu çalıştırarak SensorTag ve Intel NUC arasındaki bağlantıyı test edin:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Değiştir `{mac address}` önceki adımda elde ettiğiniz MAC adresine sahip.

## <a name="get-the-connection-string-of-sensortag"></a>SensorTag bağlantı dizesi alma

SensorTag Azure IOT hub bağlantı dizesini almak için ana bilgisayarda aşağıdaki komutu çalıştırın:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`kullandığınız IOT hub addır. IOT ağ geçidi değeri olarak kullanın `{resource group name}` ve mydevice değeri olarak `{device id}` Ders 2 değerinde değiştirilmediyse.

## <a name="configure-the-ble-sample-application"></a>BIRAK örnek uygulamayı yapılandırma

Yapılandırmak ve bırak örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:

1. Açık `config-sensortag.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Kod içinde aşağıdaki değişiklikleri yapın:
   - Değiştir `[IoT hub name]` ile kullandığınız IOT hub adı.
   - Değiştir `[IoT device connection string]` aldığınız SensorTag bağlantı dizesi ile.
   - Değiştir `[device_mac_address]` aldığınız SensorTag MAC adresine sahip.

3. BIRAK örnek uygulamayı çalıştırın.

   BIRAK örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:

   1. Üzerinde SensorTag açın.

   2. Dağıtma ve aşağıdaki komutu çalıştırarak üzerinde Intel NUC bırak örnek uygulamayı çalıştırın:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a>BIRAK örnek uygulama çalıştığını doğrulayın

Şimdi, aşağıdakine benzer bir çıktı görmeniz gerekir:

![BIRAK örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

Örnek uygulama sıcaklık veri toplamayı tutar ve IOT hub'ınıza gönderilir. Örnek uygulama, 40 saniye gönderdikten sonra otomatik olarak sona erer.

## <a name="summary"></a>Özet

Başarılı bir şekilde SensorTag ve Intel NUC arasında bağlantılar kurmak ve toplar ve veri SensorTag IOT hub'ınıza gönderir bırak örnek uygulamayı çalıştırın. IOT hub'ınızı veri aldığını doğrulamak öğrenmek hazırsınız.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ınızdan ileti okuma](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)