---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "BIRAK örnek uygulama tooreceive veri BOŞALT SensorTag ve IOT hub'ınızı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bırak uygulama, algılayıcı İzleyici uygulama, algılayıcı veri toplama, algılayıcılar, algılayıcı verileri toocloud verileri"
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
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Yapılandırma ve bırak örnek uygulamayı çalıştırma

## <a name="what-you-will-do"></a>Ne yapacağını

- Kopya hello örnek depo. 
- SensorTag ve Intel NUC arasında hello bağlantı kurun. 
- Hello Azure CLI tooget bırak (Bluetooth düşük enerji) örnek bir uygulama için IOT hub ve SensorTag bilgileri kullanın. Yapılandırmak ve hello bırak örnek uygulamayı çalıştırın. 

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu makalede, şunları öğreneceksiniz:

- Nasıl tooconfigure ve çalışma hello bırak örnek uygulama.

## <a name="what-you-need"></a>Ne gerekiyor

Başarılı bir şekilde tamamladınız gerekir

- [IOT hub'ı oluşturma ve SensorTag kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Kopya hello örnek depo toohello ana bilgisayarı

tooclone hello örnek deposu, hello ana bilgisayarda aşağıdaki adımları izleyin:

1. Windows komut istemi penceresi açın veya terminal macOS veya Ubuntu açın.
2. Merhaba aşağıdaki komutları çalıştırın:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>SensorTag ve Intel NUC arasında hello bağlantısı ayarlama

Merhaba bağlantı kurma tooset hello ana bilgisayarda aşağıdaki adımları izleyin:

1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Açık `config-gateway.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Aşağıdaki kod hello bulun ve değiştirin `[device hostname or IP address]` başlangıç IP adresi veya ana bilgisayar adı ile Intel NUC.
   ![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Yardımcı Araçlar hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC yükleyin:

   ```bash
   gulp install-tools
   ```

5. Resim aşağıdaki hello hello güç düğmesine basarak üzerinde SensorTag açın ve hello yeşil LED blink.

   ![Algılayıcı etiketi Aç](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Merhaba aşağıdaki komutları çalıştırarak SensorTag aygıtlarını tara:

   ```bash
   gulp discover-sensortag
   ```

7. Merhaba SensorTag ve Intel NUC arasında Hello bağlantısı hello aşağıdaki komutu çalıştırarak test edin:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Değiştir `{mac address}` hello hello önceki adımda elde ettiğiniz MAC adresine sahip.

## <a name="get-hello-connection-string-of-sensortag"></a>SensorTag Hello bağlantı dizesi alma

tooget hello Azure IOT hub bağlantı dizesi SensorTag, komut hello ana bilgisayarda aşağıdaki hello çalıştırın:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`kullandığınız hello IOT hub adıdır. IOT ağ geçidi hello değeri olarak kullanın `{resource group name}` ve mydevice hello değeri olarak `{device id}` Ders 2 hello değerinde değiştirilmediyse.

## <a name="configure-hello-ble-sample-application"></a>Merhaba bırak örnek uygulamayı yapılandırma

tooconfigure ve çalışma hello bırak örnek uygulama, hello ana bilgisayarda aşağıdaki adımları izleyin:

1. Açık `config-sensortag.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Merhaba kodda değişiklik aşağıdaki hello olun:
   - Değiştir `[IoT hub name]` kullandığınız hello IOT hub'ı adı ile.
   - Değiştir `[IoT device connection string]` aldığınız SensorTag hello bağlantı dizesi ile.
   - Değiştir `[device_mac_address]` hello hello aldığınız SensorTag MAC adresine sahip.

3. Merhaba bırak örnek uygulamayı çalıştırın.

   toorun hello bırak örnek uygulama, hello ana bilgisayarda aşağıdaki adımları izleyin:

   1. Üzerinde SensorTag açın.

   2. Dağıtma ve hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC hello bırak örnek uygulamayı çalıştırın:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Merhaba bırak örnek uygulaması çalıştığını doğrulayın

Şimdi hello aşağıdaki gibi bir çıktı görmeniz gerekir:

![BIRAK örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

Merhaba örnek uygulaması sıcaklık veri toplamayı tutar ve tooyour IOT hub'ı gönderilir. Merhaba örnek uygulaması, 40 saniye gönderdikten sonra otomatik olarak sona erer.

## <a name="summary"></a>Özet

Başarılı bir şekilde SensorTag ve Intel NUC arasında hello bağlantılar kurmak ve toplar ve SensorTag tooyour IOT hub'ından veri gönderen bir bırak örnek uygulamayı çalıştırın. Hazır toolearn olduğunuz nasıl IOT hub'ınızı aldı tooverify hello veri.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ınızdan ileti okuma](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)