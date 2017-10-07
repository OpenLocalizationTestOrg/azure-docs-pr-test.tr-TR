---
title: 'Connect Arduino (C) tooAzure IOT - Ders 3: Tablo depolama | Microsoft Docs'
description: "Azure Table storage'ı tooyour yazıldığı şekilde hello cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
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
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>İletileri okuma Azure Depolama'da kalıcı
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba iletileri olarak Adafruit yumuşatma M0 WiFi Arduino Panosu tooyour IOT hub'dan gönderilen İzleyicisi Merhaba cihaz bulut iletilerini tooyour Azure Table depolama yazılır.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, Azure Table storage ' nasıl toouse Merhaba gulp okuma ileti görevi tooread iletileri kalıcı öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Arduino Panonuzda hello Azure blink örnek uygulamayı çalıştırın][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Depolama hesabınızdan yeni iletiler okuma
Merhaba önceki makalede örnek uygulama Arduino Panonuzda verdi. Merhaba örnek uygulaması tooyour Azure IOT hub'ı iletileri gönderilir. tooyour IOT hub'a gönderilen Merhaba iletileri hello Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır. Azure Table storage'hello Azure depolama bağlantı dizesi tooread iletileri gerekir.

Azure Table depolama biriminde, depolanan tooread iletiler şu adımları izleyin:

1. Hello bağlantı dizesi hello aşağıdaki komutları çalıştırarak alın:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Merhaba ilk komut alır hello `storage name` hello ikinci komutu tooget hello bağlantı dizesi olarak kullanılır. Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.
2. Açık hello yapılandırma dosyası `config-arduino.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Değiştir `[Azure storage connection string]` 1. adımda aldığınız hello bağlantı dizesine sahip.
4. Merhaba Kaydet `config-arduino.json` dosya.
5. İletileri yeniden göndermek ve bunları hello aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Hello Azure Table depolama veri okuma için mantığı olan hello `azure-table.js` dosya.

   ![çalıştırma--gulp okuma depolama][gulp-run]

## <a name="summary"></a>Özet
Başarıyla Arduino tablosu tooyour IOT hub'ınızı hello bulutta bağlı ve hello blink örnek uygulama toosend cihaz bulut iletilerini kullanılır. Ayrıca, hello Azure işlevi uygulama toostore gelen IOT hub iletileri tooyour Azure Table depolama de kullanılır. Şimdi, IOT hub tooyour Arduino Panosu bulut-cihaz iletilerini gönderebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut cihaza ileti gönderme][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md