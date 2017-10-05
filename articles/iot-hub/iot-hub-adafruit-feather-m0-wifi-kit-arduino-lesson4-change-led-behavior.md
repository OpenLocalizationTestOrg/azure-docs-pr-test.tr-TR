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
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="48482-104">Açık ve kapalı LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="48482-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="48482-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="48482-105">What you will do</span></span>
<span data-ttu-id="48482-106">LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="48482-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="48482-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.</span><span class="sxs-lookup"><span data-stu-id="48482-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="48482-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="48482-108">What you will learn</span></span>
<span data-ttu-id="48482-109">LED açma ve kapatma davranışını değiştirmek için ek Arduino işlevleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="48482-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="48482-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="48482-110">What you need</span></span>
<span data-ttu-id="48482-111">Başarılı bir şekilde tamamladınız gerekir [Arduino panonuzu bulut aygıt iletileri almak için bir örnek uygulamayı çalıştırmak][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="48482-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="48482-112">Main.c ve gulpfile.js İşlevler ekleme</span><span class="sxs-lookup"><span data-stu-id="48482-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="48482-113">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="48482-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="48482-114">Açık `app.ino` dosya ve ardından aşağıdaki işlevleri sonra blinkLED() işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="48482-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="48482-116">Önce aşağıdaki koşulları ekleyin `else if` , engellemek `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="48482-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="48482-117">Şimdi, daha fazla yönerge iletileri aracılığıyla yanıtlamak için örnek uygulama yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="48482-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="48482-118">"Açık" yönerge üzerinde LED kapatır ve "kapalı" yönerge LED devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="48482-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="48482-119">Gulpfile.js dosyasını açın ve ardından yeni bir işlev işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="48482-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="48482-121">İçinde `sendMessage` işlev, satır Değiştir `var message = buildMessage(sentMessageCount);` aşağıdaki kod parçacığında gösterildiği yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="48482-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="48482-122">Tüm değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48482-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="48482-123">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="48482-123">Deploy and run the sample application</span></span>
<span data-ttu-id="48482-124">Dağıtma ve aşağıdaki komutu çalıştırarak Arduino Panonuzda örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="48482-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="48482-125">İki saniye LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48482-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="48482-126">Son "Durdur" iletisi örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="48482-126">The last "stop" message stops the sample application from running.</span></span>

![açma ve kapatma][on-and-off]

<span data-ttu-id="48482-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="48482-128">Congratulations!</span></span> <span data-ttu-id="48482-129">Başarıyla Arduino panonuzu IOT hub'ından gönderilen iletileri özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="48482-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="48482-130">Özet</span><span class="sxs-lookup"><span data-stu-id="48482-130">Summary</span></span>
<span data-ttu-id="48482-131">Bu isteğe bağlı bir bölüm, böylece örnek uygulamanın açık ve kapalı LED davranışını farklı bir şekilde denetleyebilirsiniz iletilerini özelleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="48482-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png