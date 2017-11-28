---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 4 bağlanın: iletileri alacak | Microsoft Docs"
description: "Örnek bir uygulama Edison'u üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri tooEdison, IOT hub tooblink hello LED gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Web, web üzerinden öncülük arduino denetim neden arduino denetimi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="c220f-105">Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c220f-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="c220f-106">Bu makalede, Intel Edison'u üzerinde örnek bir uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c220f-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="c220f-107">Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="c220f-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="c220f-108">Ayrıca bir gulp görev, bilgisayar toosend iletileri tooEdison IOT hub'ından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c220f-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="c220f-109">Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="c220f-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="c220f-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c220f-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c220f-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="c220f-111">What you will do</span></span>
* <span data-ttu-id="c220f-112">Merhaba örnek uygulama tooyour IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c220f-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="c220f-113">Dağıtma ve hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c220f-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="c220f-114">İletiler, IOT hub tooEdison tooblink hello LED gönderin.</span><span class="sxs-lookup"><span data-stu-id="c220f-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c220f-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="c220f-115">What you will learn</span></span>
<span data-ttu-id="c220f-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="c220f-116">In this article, you will learn:</span></span>
* <span data-ttu-id="c220f-117">Nasıl IOT hub'ından toomonitor gelen iletileri.</span><span class="sxs-lookup"><span data-stu-id="c220f-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="c220f-118">Nasıl toosend bulut-cihaz, IOT hub tooEdison iletileri.</span><span class="sxs-lookup"><span data-stu-id="c220f-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c220f-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c220f-119">What you need</span></span>
* <span data-ttu-id="c220f-120">Intel Edison'u ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c220f-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="c220f-121">tooset Edison'u, Yukarı nasıl görürüm toolearn [Cihazınızı yapılandırmak][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="c220f-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="c220f-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="c220f-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="c220f-123">toolearn nasıl toocreate IOT hub'ınızı bkz [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="c220f-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="c220f-124">Merhaba örnek uygulama tooyour IOT hub'ı Bağlan</span><span class="sxs-lookup"><span data-stu-id="c220f-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="c220f-125">Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="c220f-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="c220f-126">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="c220f-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="c220f-127">Merhaba Hello dosyasında `app` alt hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="c220f-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="c220f-128">Merhaba `blinkLED` işlevi yanıp hello LED.</span><span class="sxs-lookup"><span data-stu-id="c220f-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Depodaki yapısında Merhaba örnek uygulaması][repo-structure]
2. <span data-ttu-id="c220f-130">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="c220f-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="c220f-131">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma hello adım toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınan ve Merhaba örnek uygulama çalıştırılıyor.</span><span class="sxs-lookup"><span data-stu-id="c220f-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="c220f-132">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-edison.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="c220f-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="c220f-133">Merhaba `config-edison.json` giriş klasörü hello alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="c220f-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Merhaba config edison.json dosyasının içeriği](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="c220f-135">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında hello cihaz IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="c220f-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="c220f-136">Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.</span><span class="sxs-lookup"><span data-stu-id="c220f-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="c220f-137">Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="c220f-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c220f-138">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c220f-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="c220f-139">Dağıtma ve hello aşağıdaki komutları çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c220f-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="c220f-140">Merhaba gulp komutu hello örnek uygulama tooEdison dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c220f-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="c220f-141">Ardından, onu Merhaba uygulaması Edison'u ve ana bilgisayarınızda ayrı bir görev bilgisayar toosend 20 blink iletileri tooEdison IOT hub'ından çalışır.</span><span class="sxs-lookup"><span data-stu-id="c220f-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="c220f-142">Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="c220f-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="c220f-143">Bu sırada, hello gulp görev, IOT hub tooEdison birkaç "blink" iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="c220f-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="c220f-144">Edison'u alan her blink ileti için hello örnek uygulama çağırır hello `blinkLED` işlevi tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="c220f-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="c220f-145">Görev gönderir 20 iletilerden IOT hub tooEdison gulp hello LED blink her iki saniye hello olarak görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c220f-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="c220f-146">Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.</span><span class="sxs-lookup"><span data-stu-id="c220f-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="c220f-148">Özet</span><span class="sxs-lookup"><span data-stu-id="c220f-148">Summary</span></span>
<span data-ttu-id="c220f-149">İleti, IOT hub tooEdison tooblink hello LED başarıyla gönderdik.</span><span class="sxs-lookup"><span data-stu-id="c220f-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="c220f-150">Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c220f-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c220f-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c220f-151">Next steps</span></span>
<span data-ttu-id="c220f-152">[Merhaba açma ve kapatma hello LED davranışını değiştirme][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="c220f-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md