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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="0d6ed-104">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0d6ed-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0d6ed-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="0d6ed-105">What you will do</span></span>
<span data-ttu-id="0d6ed-106">Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="0d6ed-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0d6ed-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0d6ed-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="0d6ed-108">What you will learn</span></span>
<span data-ttu-id="0d6ed-109">Ek Node.js işlevleri toochange hello LED açma ve Kapatma davranışı kullanıcının kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0d6ed-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0d6ed-110">What you need</span></span>
<span data-ttu-id="0d6ed-111">Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama toodevice iletileri Raspberry Pi'yi tooreceive bulutta çalışacak](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="0d6ed-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="0d6ed-112">İşlevler toomain.c ve gulpfile.js ekleyin</span><span class="sxs-lookup"><span data-stu-id="0d6ed-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="0d6ed-113">Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="0d6ed-114">Açık hello `main.c` dosya ve işlevleri blinkLED() işlevi sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="0d6ed-116">Hello koşullar hello varsayılan önce aşağıdaki hello eklemek `if` hello bloğunu `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-116">Add hello following conditions before hello default one in hello `if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="0d6ed-117">Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="0d6ed-118">Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="0d6ed-119">Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="0d6ed-121">Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="0d6ed-122">Tüm hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="0d6ed-123">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0d6ed-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="0d6ed-124">Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0d6ed-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="0d6ed-125">İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="0d6ed-126">Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-126">hello last "stop" message stops hello sample application from running.</span></span>

![Örnek uygulama ile açma ve kapatma iletileri](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="0d6ed-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0d6ed-128">Congratulations!</span></span> <span data-ttu-id="0d6ed-129">TooPi IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="0d6ed-130">Özet</span><span class="sxs-lookup"><span data-stu-id="0d6ed-130">Summary</span></span>
<span data-ttu-id="0d6ed-131">İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0d6ed-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>
