---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 4: uygulama değiştirme | Microsoft Docs"
description: "Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin."
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
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Merhaba açma ve kapatma hello LED davranışını değiştirme
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Ek Node.js işlevleri toochange hello LED açma ve Kapatma davranışı kullanıcının kullanın.

## <a name="what-you-need"></a>Ne gerekiyor
Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama toodevice iletileri Raspberry Pi'yi tooreceive bulutta çalışacak](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-toomainc-and-gulpfilejs"></a>İşlevler toomain.c ve gulpfile.js ekleyin
1. Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:

   ```bash
   cd Lesson4
   code .
   ```
2. Açık hello `main.c` dosya ve işlevleri blinkLED() işlevi sonra aşağıdaki hello ekleyin:

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
3. Hello koşullar hello varsayılan önce aşağıdaki hello eklemek `if` hello bloğunu `receiveMessageCallback` işlevi:

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

   Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız. Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.
4. Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:

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
5. Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Tüm hello değişiklikleri kaydedin.

### <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir. Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.

![Örnek uygulama ile açma ve kapatma iletileri](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Tebrikler! TooPi IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.

### <a name="summary"></a>Özet
İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.
