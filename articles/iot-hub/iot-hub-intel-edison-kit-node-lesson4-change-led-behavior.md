---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 4 bağlanın: Blink hello LED | Microsoft Docs"
description: "Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ile arduino öncülük denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="d9261-104">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="d9261-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d9261-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="d9261-105">What you will do</span></span>
<span data-ttu-id="d9261-106">Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9261-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="d9261-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d9261-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d9261-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="d9261-108">What you will learn</span></span>
<span data-ttu-id="d9261-109">Açma ve Kapatma davranışı LED kullanıcının ek işlevler toochange hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9261-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d9261-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="d9261-110">What you need</span></span>
<span data-ttu-id="d9261-111">Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama toodevice iletileri Intel Edison'u tooreceive bulutta çalışacak][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="d9261-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="d9261-112">İşlevler tooapp.js ve gulpfile.js ekleyin</span><span class="sxs-lookup"><span data-stu-id="d9261-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="d9261-113">Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="d9261-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="d9261-114">Açık hello `app.js` dosya ve işlevleri blinkLED() işlevi sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d9261-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![App.js dosyasıyla eklenen İşlevler](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="d9261-116">Merhaba hello önce aşağıdaki koşulların 'blink' hello anahtar durumu hello bloğunu durumda eklemek `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="d9261-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="d9261-117">Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="d9261-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="d9261-118">Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="d9261-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="d9261-119">Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="d9261-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="d9261-121">Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="d9261-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="d9261-122">Tüm hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d9261-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d9261-123">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d9261-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="d9261-124">Dağıtma ve hello aşağıdaki komutu çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d9261-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="d9261-125">İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9261-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="d9261-126">Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="d9261-126">hello last "stop" message stops hello sample application from running.</span></span>

![açma ve kapatma][on-and-off]

<span data-ttu-id="d9261-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="d9261-128">Congratulations!</span></span> <span data-ttu-id="d9261-129">TooEdison IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="d9261-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="d9261-130">Özet</span><span class="sxs-lookup"><span data-stu-id="d9261-130">Summary</span></span>
<span data-ttu-id="d9261-131">İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9261-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
