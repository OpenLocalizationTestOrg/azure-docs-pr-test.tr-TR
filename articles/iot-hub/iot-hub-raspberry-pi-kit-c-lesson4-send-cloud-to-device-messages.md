---
title: 'Connect Raspberry pi (C) tooAzure IOT - Ders 4: Bulut cihaz | Microsoft Docs'
description: "Örnek bir uygulama Pi üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri tooPi, IOT hub tooblink hello LED gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toodevice bulut, buluttan ileti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="26401-105">Örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="26401-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="26401-106">Bu makalede, Raspberry Pi 3 örnek bir uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="26401-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="26401-107">Merhaba örnek uygulaması IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="26401-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="26401-108">Ayrıca bir gulp görev, bilgisayar toosend iletileri tooPi IOT hub'ından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="26401-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="26401-109">Merhaba örnek uygulaması Merhaba iletileri aldığında, hello ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="26401-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="26401-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="26401-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="26401-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="26401-111">What you will do</span></span>
* <span data-ttu-id="26401-112">Merhaba örnek uygulama tooyour IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="26401-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="26401-113">Dağıtma ve hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="26401-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="26401-114">İletiler, IOT hub tooPi tooblink hello LED gönderin.</span><span class="sxs-lookup"><span data-stu-id="26401-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="26401-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="26401-115">What you will learn</span></span>
<span data-ttu-id="26401-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="26401-116">In this article, you will learn:</span></span>
* <span data-ttu-id="26401-117">Nasıl IOT hub'ından toomonitor gelen iletileri.</span><span class="sxs-lookup"><span data-stu-id="26401-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="26401-118">Nasıl toosend bulut-cihaz, IOT hub tooPi iletileri.</span><span class="sxs-lookup"><span data-stu-id="26401-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="26401-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="26401-119">What you need</span></span>
* <span data-ttu-id="26401-120">Böğürtlenli Pi 3 ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="26401-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="26401-121">Pi yukarı tooset nasıl görürüm toolearn [Cihazınızı yapılandırmak](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="26401-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="26401-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="26401-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="26401-123">toolearn nasıl toocreate IOT hub'ınızı bkz [IOT hub'ınızı oluşturma ve Raspberry Pi 3 kaydetme](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="26401-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="26401-124">Merhaba örnek uygulama tooyour IOT hub'ı Bağlan</span><span class="sxs-lookup"><span data-stu-id="26401-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="26401-125">Merhaba depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="26401-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="26401-126">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="26401-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="26401-127">Bildirim hello `app.c` hello dosyasında `app` alt klasörü.</span><span class="sxs-lookup"><span data-stu-id="26401-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="26401-128">Merhaba `app.c` hello kod toomonitor gelen iletilere hello IOT hub'ı içeren hello anahtar kaynak dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="26401-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="26401-129">Merhaba `blinkLED` işlevi yanıp hello LED.</span><span class="sxs-lookup"><span data-stu-id="26401-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Depodaki yapısında Merhaba örnek uygulaması](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="26401-131">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="26401-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="26401-132">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) dağıtma ve çalıştırmanın Merhaba örnek uygulaması toostep toohello görev atlayabilirsiniz bu bilgisayarda tüm hello yapılandırmaları, devralınır.</span><span class="sxs-lookup"><span data-stu-id="26401-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="26401-133">Merhaba adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) başka bir bilgisayara ihtiyacınız hello tooreplace hello yer tutucuları `config-raspberrypi.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="26401-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="26401-134">Merhaba `config-raspberrypi.json` giriş klasörü hello alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="26401-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Merhaba config raspberrypi.json dosyasının içeriği](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="26401-136">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** hello çalıştırarak aldığınız Pı'nin IP adresi veya ana bilgisayar adı ile `devdisco list --eth` komutu.</span><span class="sxs-lookup"><span data-stu-id="26401-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="26401-137">Değiştir **[IOT cihaz bağlantı dizesi]** hello cihaz bağlantı dizesiyle hello çalıştırarak aldığınız `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="26401-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="26401-138">Değiştir **[IOT hub bağlantı dizesine]** hello hello çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="26401-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="26401-139">Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="26401-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="26401-140">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="26401-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="26401-141">Dağıtma ve hello aşağıdaki komutları çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="26401-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="26401-142">Merhaba gulp komutu çalıştırır yükleme araçları görev ilk hello.</span><span class="sxs-lookup"><span data-stu-id="26401-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="26401-143">Ardından hello örnek uygulama tooPi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="26401-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="26401-144">Son olarak, bu Merhaba uygulaması Pi ve ayrı bir görev, ana bilgisayardaki bilgisayar toosend 20 blink iletileri tooPi IOT hub'ından çalışır.</span><span class="sxs-lookup"><span data-stu-id="26401-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="26401-145">Merhaba örnek uygulaması çalıştıktan sonra IOT hub'dan toomessages dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="26401-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="26401-146">Bu sırada, hello gulp görev, IOT hub tooPi birkaç "blink" iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="26401-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="26401-147">Pi alan her blink ileti için hello örnek uygulama çağırır hello `blinkLED` işlevi tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="26401-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="26401-148">Görev gönderir 20 iletilerden IOT hub tooPi gulp hello LED blink her iki saniye hello olarak görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26401-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="26401-149">Merhaba son hello uygulamanın çalışmasını durdurur "Durdur" bir ileti biridir.</span><span class="sxs-lookup"><span data-stu-id="26401-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="26401-151">Özet</span><span class="sxs-lookup"><span data-stu-id="26401-151">Summary</span></span>
<span data-ttu-id="26401-152">İleti, IOT hub tooPi tooblink hello LED başarıyla gönderdik.</span><span class="sxs-lookup"><span data-stu-id="26401-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="26401-153">Merhaba sonraki görev, isteğe bağlı: hello açma ve kapatma hello LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="26401-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26401-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26401-154">Next steps</span></span>
[<span data-ttu-id="26401-155">Merhaba açma ve kapatma hello LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="26401-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
