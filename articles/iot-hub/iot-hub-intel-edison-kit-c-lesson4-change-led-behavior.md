---
title: 'Connect Intel Edison (C) tooAzure IOT - Ders 4: Blink hello LED | Microsoft Docs'
description: "Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin."
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
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="81af8-104">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="81af8-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="81af8-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="81af8-105">What you will do</span></span>
<span data-ttu-id="81af8-106">Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="81af8-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="81af8-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="81af8-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="81af8-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="81af8-108">What you will learn</span></span>
<span data-ttu-id="81af8-109">Açma ve Kapatma davranışı LED kullanıcının ek işlevler toochange hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="81af8-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81af8-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="81af8-110">What you need</span></span>
<span data-ttu-id="81af8-111">Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama toodevice iletileri Intel Edison'u tooreceive bulutta çalışacak][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="81af8-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="81af8-112">İşlevler toomain.c ve gulpfile.js ekleyin</span><span class="sxs-lookup"><span data-stu-id="81af8-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="81af8-113">Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="81af8-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="81af8-114">Açık hello `main.c` dosya ve işlevleri blinkLED() işlevi sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="81af8-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="81af8-116">Koşullar hello önce aşağıdaki hello eklemek `else if` hello bloğunu `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="81af8-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="81af8-117">Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="81af8-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="81af8-118">Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="81af8-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="81af8-119">Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="81af8-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="81af8-121">Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="81af8-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="81af8-122">Tüm hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="81af8-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="81af8-123">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="81af8-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="81af8-124">Dağıtma ve hello aşağıdaki komutu çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="81af8-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="81af8-125">İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="81af8-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="81af8-126">Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="81af8-126">hello last "stop" message stops hello sample application from running.</span></span>

![açma ve kapatma][on-and-off]

<span data-ttu-id="81af8-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="81af8-128">Congratulations!</span></span> <span data-ttu-id="81af8-129">TooEdison IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="81af8-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="81af8-130">Özet</span><span class="sxs-lookup"><span data-stu-id="81af8-130">Summary</span></span>
<span data-ttu-id="81af8-131">İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="81af8-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
