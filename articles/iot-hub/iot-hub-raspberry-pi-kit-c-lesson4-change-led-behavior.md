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
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="6fe42-104">Açık ve kapalı LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6fe42-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6fe42-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="6fe42-105">What you will do</span></span>
<span data-ttu-id="6fe42-106">LED açma ve kapatma davranışını değiştirmek için iletilerini özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6fe42-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="6fe42-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6fe42-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6fe42-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="6fe42-108">What you will learn</span></span>
<span data-ttu-id="6fe42-109">LED açma ve kapatma davranışını değiştirmek için ek Node.js işlevleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fe42-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6fe42-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="6fe42-110">What you need</span></span>
<span data-ttu-id="6fe42-111">Başarılı bir şekilde tamamladınız gerekir [Raspberry Pi'yi bulut aygıt iletileri almak için bir örnek uygulamayı çalıştırmak](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6fe42-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud to device messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="6fe42-112">Main.c ve gulpfile.js İşlevler ekleme</span><span class="sxs-lookup"><span data-stu-id="6fe42-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="6fe42-113">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="6fe42-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="6fe42-114">Açık `main.c` dosya ve ardından aşağıdaki işlevleri sonra blinkLED() işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6fe42-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="6fe42-116">Varsayılan önce aşağıdaki koşulları ekleyin `if` , engellemek `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="6fe42-116">Add the following conditions before the default one in the `if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="6fe42-117">Şimdi, daha fazla yönerge iletileri aracılığıyla yanıtlamak için örnek uygulama yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="6fe42-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="6fe42-118">"Açık" yönerge üzerinde LED kapatır ve "kapalı" yönerge LED devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="6fe42-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="6fe42-119">Gulpfile.js dosyasını açın ve ardından yeni bir işlev işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="6fe42-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="6fe42-121">İçinde `sendMessage` işlev, satır Değiştir `var message = buildMessage(sentMessageCount);` aşağıdaki kod parçacığında gösterildiği yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="6fe42-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="6fe42-122">Tüm değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6fe42-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="6fe42-123">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6fe42-123">Deploy and run the sample application</span></span>
<span data-ttu-id="6fe42-124">Dağıtma ve aşağıdaki komutu çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6fe42-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="6fe42-125">İki saniye LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fe42-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="6fe42-126">Son "Durdur" iletisi örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="6fe42-126">The last "stop" message stops the sample application from running.</span></span>

![Örnek uygulama ile açma ve kapatma iletileri](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="6fe42-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6fe42-128">Congratulations!</span></span> <span data-ttu-id="6fe42-129">Pi IOT hub'ından gönderilen iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe42-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="6fe42-130">Özet</span><span class="sxs-lookup"><span data-stu-id="6fe42-130">Summary</span></span>
<span data-ttu-id="6fe42-131">Bu isteğe bağlı bir bölüm, böylece örnek uygulamanın açık ve kapalı LED davranışını farklı bir şekilde denetleyebilirsiniz iletilerini özelleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6fe42-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>
