---
title: "Azure IOT - Ders 4 Intel Edison (C) bağlanın: LED Blink | Microsoft Docs"
description: "LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ile arduino öncülük denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Açık ve kapalı LED davranışını değiştirme
## <a name="what-you-will-do"></a>Ne yapacağını
LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
LED açma ve kapatma davranışını değiştirmek için ek işlevler kullanın.

## <a name="what-you-need"></a>Ne gerekiyor
Başarılı bir şekilde tamamladınız gerekir [bulut aygıt iletileri almak için Intel Edison'u bir örnek uygulamayı çalıştırmak][receive-cloud-to-device-messages].

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
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![Main.c dosyasıyla eklenen İşlevler](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Önce aşağıdaki koşulları ekleyin `else if` , engellemek `receiveMessageCallback` işlevi:

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

   ![Gulpfile.js dosyasıyla eklenen işlevi][gulpfile]
5. İçinde `sendMessage` işlev, satır Değiştir `var message = buildMessage(sentMessageCount);` aşağıdaki kod parçacığında gösterildiği yeni satır ile:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Tüm değişiklikleri kaydedin.

### <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak Edison'u üzerinde örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

İki saniye LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir. Son "Durdur" iletisi örnek uygulamanın çalışmasını durdurur.

![açma ve kapatma][on-and-off]

Tebrikler! Başarıyla Edison'u için IOT hub'ından gönderilen iletileri özelleştirdiğiniz.

### <a name="summary"></a>Özet
Bu isteğe bağlı bir bölüm, böylece örnek uygulamanın açık ve kapalı LED davranışını farklı bir şekilde denetleyebilirsiniz iletilerini özelleştirmek gösterilmiştir.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
