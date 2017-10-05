---
title: "Azure IOT - Ders 4 Arduino (C) bağlanın: uygulama değiştirme | Microsoft Docs"
description: "LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ile arduino öncülük denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Açık ve kapalı LED davranışını değiştirme
## <a name="what-you-will-do"></a>Ne yapacağını
LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
LED açma ve kapatma davranışını değiştirmek için ek Arduino işlevleri kullanın.

## <a name="what-you-need"></a>Ne gerekiyor
Başarılı bir şekilde tamamladınız gerekir [Arduino panonuzu bulut aygıt iletileri almak için bir örnek uygulamayı çalıştırmak][receive-cloud-to-device-messages].

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Main.c ve gulpfile.js İşlevler ekleme
1. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio code'da açın:

   ```bash
   cd Lesson4
   code .
   ```
2. Açık `app.ino` dosya ve ardından aşağıdaki işlevleri sonra blinkLED() işlevi ekleyin:

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![app.ino dosyasıyla eklenen İşlevler][app-ino-file]
3. Önce aşağıdaki koşulları ekleyin `else if` , engellemek `receiveMessageCallback` işlevi:

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Şimdi, daha fazla yönerge iletileri aracılığıyla yanıtlamak için örnek uygulama yapılandırdığınız. "Açık" yönerge üzerinde LED kapatır ve "kapalı" yönerge LED devre dışı bırakır.
4. Gulpfile.js dosyasını açın ve ardından yeni bir işlev işlevi önce ekleyin `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Gulpfile.js dosyasıyla eklenen işlevi][gulp-file-js]
5. İçinde `sendMessage` işlev, satır Değiştir `var message = buildMessage(sentMessageCount);` aşağıdaki kod parçacığında gösterildiği yeni satır ile:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Tüm değişiklikleri kaydedin.

### <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak Arduino Panonuzda örnek uygulamayı çalıştırın:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

İki saniye LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir. Son "Durdur" iletisi örnek uygulamanın çalışmasını durdurur.

![açma ve kapatma][on-and-off]

Tebrikler! Başarıyla Arduino panonuzu IOT hub'ından gönderilen iletileri özelleştirdiğiniz.

### <a name="summary"></a>Özet
Bu isteğe bağlı bir bölüm, böylece örnek uygulamanın açık ve kapalı LED davranışını farklı bir şekilde denetleyebilirsiniz iletilerini özelleştirmek gösterilmiştir.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png