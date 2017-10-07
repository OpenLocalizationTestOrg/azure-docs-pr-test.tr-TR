---
title: "Connect Arduino (C) tooAzure IOT - Ders 4: uygulama değiştirme | Microsoft Docs"
description: "Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin."
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
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="987a5-104">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="987a5-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="987a5-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="987a5-105">What you will do</span></span>
<span data-ttu-id="987a5-106">Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="987a5-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="987a5-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.</span><span class="sxs-lookup"><span data-stu-id="987a5-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="987a5-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="987a5-108">What you will learn</span></span>
<span data-ttu-id="987a5-109">Ek Arduino işlevleri toochange hello LED açma ve Kapatma davranışı kullanıcının kullanın.</span><span class="sxs-lookup"><span data-stu-id="987a5-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="987a5-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="987a5-110">What you need</span></span>
<span data-ttu-id="987a5-111">Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama toodevice iletileri Arduino Panosu tooreceive bulut üzerinde çalıştırmak][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="987a5-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="987a5-112">İşlevler toomain.c ve gulpfile.js ekleyin</span><span class="sxs-lookup"><span data-stu-id="987a5-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="987a5-113">Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="987a5-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="987a5-114">Açık hello `app.ino` dosya ve işlevleri blinkLED() işlevi sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="987a5-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="987a5-116">Koşullar hello önce aşağıdaki hello eklemek `else if` hello bloğunu `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="987a5-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="987a5-117">Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="987a5-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="987a5-118">Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="987a5-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="987a5-119">Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="987a5-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="987a5-121">Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="987a5-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="987a5-122">Tüm hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="987a5-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="987a5-123">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="987a5-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="987a5-124">Dağıtma ve hello aşağıdaki komutu çalıştırarak Arduino Panonuzda hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="987a5-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="987a5-125">İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="987a5-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="987a5-126">Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="987a5-126">hello last "stop" message stops hello sample application from running.</span></span>

![açma ve kapatma][on-and-off]

<span data-ttu-id="987a5-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="987a5-128">Congratulations!</span></span> <span data-ttu-id="987a5-129">Tooyour Arduino Panosu IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="987a5-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="987a5-130">Özet</span><span class="sxs-lookup"><span data-stu-id="987a5-130">Summary</span></span>
<span data-ttu-id="987a5-131">İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="987a5-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png