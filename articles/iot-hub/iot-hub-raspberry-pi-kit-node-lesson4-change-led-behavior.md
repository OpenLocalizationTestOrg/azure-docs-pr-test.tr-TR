---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 4 bağlanın: uygulama değiştirme | Microsoft Docs"
description: "Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Denetim ile Böğürtlenli pi, Böğürtlenli öncülük pi denetimi, Böğürtlenli pi denetimi neden neden"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="17e51-104">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="17e51-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="17e51-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="17e51-105">What you will do</span></span>
<span data-ttu-id="17e51-106">Merhaba iletileri toochange hello LED açma ve Kapatma davranışı kullanıcının özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="17e51-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="17e51-107">Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="17e51-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="17e51-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="17e51-108">What you will learn</span></span>
<span data-ttu-id="17e51-109">Ek Node.js işlevleri toochange hello LED açma ve Kapatma davranışı kullanıcının kullanın.</span><span class="sxs-lookup"><span data-stu-id="17e51-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="17e51-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="17e51-110">What you need</span></span>
<span data-ttu-id="17e51-111">Başarılı bir şekilde tamamladınız gerekir [örnek bir uygulama üzerinde Raspberry Pi'yi tooreceive bulut-cihaz iletilerini çalıştırmak](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="17e51-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="17e51-112">Node.js İşlevler ekleme</span><span class="sxs-lookup"><span data-stu-id="17e51-112">Add Node.js functions</span></span>
1. <span data-ttu-id="17e51-113">Merhaba örnek uygulaması hello aşağıdaki komutları çalıştırarak Visual Studio code'da açın:</span><span class="sxs-lookup"><span data-stu-id="17e51-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="17e51-114">Açık hello `app.js` dosya ve işlevleri hello sonunda aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="17e51-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![App.js dosyasıyla eklenen İşlevler](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="17e51-116">Merhaba anahtar durumu bloğunda hello koşullar hello varsayılan önce aşağıdaki hello eklemek `receiveMessageCallback` işlevi:</span><span class="sxs-lookup"><span data-stu-id="17e51-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="17e51-117">Şimdi, hello örnek uygulama toorespond toomore yönergeleri iletileri aracılığıyla yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="17e51-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="17e51-118">Merhaba "açık" yönerge LED hello üzerinde kapatır ve "kapalı" yönerge hello LED hello devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="17e51-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="17e51-119">Merhaba gulpfile.js dosyasını açın ve ardından yeni bir işlev hello işlevi önce ekleyin `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="17e51-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
   
   ![Gulpfile.js dosyasıyla eklenen işlevi](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="17e51-121">Merhaba, `sendMessage` işlev, hello satırını değiştirmek `var message = buildMessage(sentMessageCount);` hello aşağıdaki kod parçacığında gösterildiği hello yeni satır ile:</span><span class="sxs-lookup"><span data-stu-id="17e51-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="17e51-122">Tüm hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="17e51-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="17e51-123">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="17e51-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="17e51-124">Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="17e51-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="17e51-125">İki saniye hello LED etkinleştirin ve başka bir iki saniye sonra Kapat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="17e51-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="17e51-126">Merhaba son "Durdur" iletisi hello örnek uygulamanın çalışmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="17e51-126">hello last "stop" message stops hello sample application from running.</span></span>

![Örnek uygulama ile açma ve kapatma iletileri](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="17e51-128">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="17e51-128">Congratulations!</span></span> <span data-ttu-id="17e51-129">TooPi IOT hub'ından gönderilen Merhaba iletileri başarıyla özelleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="17e51-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="17e51-130">Özet</span><span class="sxs-lookup"><span data-stu-id="17e51-130">Summary</span></span>
<span data-ttu-id="17e51-131">İsteğe bağlı Bu bölüm, böylece Merhaba örnek uygulaması farklı bir şekilde hello açma ve kapatma hello LED davranışını kontrol edebilirsiniz toocustomize nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="17e51-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

