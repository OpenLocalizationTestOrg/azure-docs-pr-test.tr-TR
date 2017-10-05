---
title: "Azure IOT - Ders 4 Böğürtlenli Pi (C) bağlanın: uygulama değiştirme | Microsoft Docs"
description: "LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Denetim ile Böğürtlenli pi, Böğürtlenli öncülük pi denetimi, Böğürtlenli pi denetimi neden neden"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Açık ve kapalı LED davranışını değiştirme
## <a name="what-you-will-do"></a>Ne yapacağını
LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
LED açma ve kapatma davranışını değiştirmek için ek Node.js işlevleri kullanın.

## <a name="what-you-need"></a>Ne gerekiyor
Başarılı bir şekilde tamamladınız gerekir [Raspberry Pi'yi bulut aygıt iletileri almak için bir örnek uygulamayı çalıştırmak](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Main.c ve gulpfile.js İşlevler ekleme
1. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio code'da açın:

   ```bash
   cd Lesson4
   code .
   ```
2. Açık `main.c` dosya ve ardından aşağıdaki işlevleri sonra blinkLED() işlevi ekleyin:

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Main.c dosyasıyla eklenen İşlevler](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. Varsayılan önce aşağıdaki koşulları ekleyin `if` , engellemek `receiveMessageCallback` işlevi:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
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
   }
   ```

   ![Gulpfile.js dosyasıyla eklenen işlevi](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. İçinde `sendMessage` işlev, satır Değiştir `var message = buildMessage(sentMessageCount);` aşağıdaki kod parçacığında gösterildiği yeni satır ile:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Tüm değişiklikleri kaydedin.

### <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

İki saniye LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir. Son "Durdur" iletisi örnek uygulamanın çalışmasını durdurur.

![Örnek uygulama ile açma ve kapatma iletileri](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Tebrikler! Pi IOT hub'ından gönderilen iletileri başarıyla özelleştirdiğiniz.

### <a name="summary"></a>Özet
Bu isteğe bağlı bir bölüm, böylece örnek uygulamanın açık ve kapalı LED davranışını farklı bir şekilde denetleyebilirsiniz iletilerini özelleştirmek gösterilmiştir.
