---
title: 'Azure IOT - Ders 3 Connect Arduino (C): Tablo depolama | Microsoft Docs'
description: "Azure Table depolama alanına yazılır gibi cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>İletileri okuma Azure Depolama'da kalıcı
## <a name="what-you-will-do"></a>Ne yapacağını
İletileri Azure Table depolama alanına yazılır gibi Adafruit yumuşatma M0 WiFi Arduino panonuzu IOT hub'ına gönderilen cihaz bulut iletilerini izleyin.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, gulp okuma ileti görevi iletileri, Azure tablo Depolama'da kalıcı okumak için nasıl kullanılacağını öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Arduino Panonuzda Azure blink örnek uygulamayı çalıştırın][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Depolama hesabınızdan yeni iletiler okuma
Önceki makalede örnek uygulama Arduino Panonuzda verdi. Azure IOT hub'ınıza örnek uygulama gönderilen iletileri. IOT hub'ına gönderilen iletileri Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır. Azure Table depolama hesabınızdan iletileri okumak için Azure depolama bağlantı dizesi gerekir.

Azure Table storage'da depolanan iletileri okumak için şu adımları izleyin:

1. Bağlantı dizesi, aşağıdaki komutları çalıştırarak alın:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   İlk komut alır `storage name` , ikinci komutta bağlantı dizesini almak için kullanılır. Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.
2. Yapılandırma dosyasını açın `config-arduino.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Değiştir `[Azure storage connection string]` 1. adımda aldığınız bağlantı dizesiyle.
4. Kaydet `config-arduino.json` dosya.
5. İletileri yeniden göndermek ve bunları aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Azure Table depolama veri okuma mantığını bulunduğu `azure-table.js` dosya.

   ![çalıştırma--gulp okuma depolama][gulp-run]

## <a name="summary"></a>Özet
Başarılı bir şekilde bulutta IOT hub'ınıza Arduino panonuzu bağlı ve cihaz bulut iletilerini göndermek için kullanılan blink örnek uygulama. Azure işlev uygulaması, Azure Table depolama alanına gelen IOT hub iletileri depolamak için de kullanılır. Şimdi, IOT hub'ından Arduino panonuzu bulut cihaz iletileri gönderebilir.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut cihaza ileti gönderme][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md