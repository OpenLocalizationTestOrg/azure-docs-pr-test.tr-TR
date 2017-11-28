---
title: "Azure IOT - Ders 4 Böğürtlenli Pi (C) bağlanın: Bulut cihaz | Microsoft Docs"
description: "Örnek bir uygulama Pi üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev, IOT hub ' LED blink Pi iletileri gönderir."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: cihaz, bulut iletiden bulut
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
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="33cc0-105">Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="33cc0-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="33cc0-106">Bu makalede, Raspberry Pi 3 örnek bir uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="33cc0-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="33cc0-107">Örnek uygulama IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="33cc0-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="33cc0-108">Ayrıca, IOT hub'ından Pi iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="33cc0-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="33cc0-109">Örnek uygulama iletileri aldığında ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="33cc0-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="33cc0-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="33cc0-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="33cc0-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="33cc0-111">What you will do</span></span>
* <span data-ttu-id="33cc0-112">Örnek uygulama IOT hub'ınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="33cc0-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="33cc0-113">Dağıtma ve örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="33cc0-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="33cc0-114">İletileri LED blink Pi için IOT hub'ından gönderin.</span><span class="sxs-lookup"><span data-stu-id="33cc0-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="33cc0-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="33cc0-115">What you will learn</span></span>
<span data-ttu-id="33cc0-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="33cc0-116">In this article, you will learn:</span></span>
* <span data-ttu-id="33cc0-117">IOT hub'ınızı gelen iletilere izlemek nasıl.</span><span class="sxs-lookup"><span data-stu-id="33cc0-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="33cc0-118">Pi IOT hub'ından bulut-cihaz iletilerini göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="33cc0-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="33cc0-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="33cc0-119">What you need</span></span>
* <span data-ttu-id="33cc0-120">Böğürtlenli Pi 3 ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="33cc0-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="33cc0-121">Pi ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="33cc0-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="33cc0-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="33cc0-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="33cc0-123">IOT hub'ınızı oluşturmayı öğrenmek için bkz: [IOT hub'ınızı oluşturma ve Raspberry Pi 3 kaydetme](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="33cc0-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="33cc0-124">Örnek uygulama IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="33cc0-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="33cc0-125">Depodaki klasöründe olduğunuzdan emin olun `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="33cc0-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="33cc0-126">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="33cc0-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="33cc0-127">Bildirim `app.c` dosyasını `app` alt klasörü.</span><span class="sxs-lookup"><span data-stu-id="33cc0-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="33cc0-128">`app.c` IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="33cc0-129">`blinkLED` İşlevi yanıp LED.</span><span class="sxs-lookup"><span data-stu-id="33cc0-129">The `blinkLED` function blinks the LED.</span></span>

   ![Depodaki yapısında örnek uygulama](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="33cc0-131">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="33cc0-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="33cc0-132">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) dağıtma ve örnek uygulama çalıştırılıyor göreve adıma atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="33cc0-133">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) yer tutucuları değiştirmek gereken başka bir bilgisayara `config-raspberrypi.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="33cc0-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="33cc0-134">`config-raspberrypi.json` Giriş klasörü alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Config raspberrypi.json dosyasının içeriği](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="33cc0-136">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** çalıştırarak aldığınız Pı'nin IP adresi veya ana bilgisayar adı ile `devdisco list --eth` komutu.</span><span class="sxs-lookup"><span data-stu-id="33cc0-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="33cc0-137">Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="33cc0-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="33cc0-138">Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="33cc0-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="33cc0-139">Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="33cc0-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="33cc0-140">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="33cc0-140">Deploy and run the sample application</span></span>
<span data-ttu-id="33cc0-141">Dağıtma ve aşağıdaki komutları çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="33cc0-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="33cc0-142">Gulp komutu ilk yükleme araçları görev çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="33cc0-143">Ardından Pi örnek uygulamayı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="33cc0-144">Son olarak, bu uygulama Pi ve ana bilgisayarınızda ayrı bir görev IOT hub'ından Pi 20 blink iletileri göndermeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="33cc0-145">Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="33cc0-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="33cc0-146">Bu sırada, gulp görev birkaç "blink" Pi için IOT hub'ınızı gelen iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="33cc0-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="33cc0-147">Pi alan her blink ileti için örnek uygulama çağırır `blinkLED` LED blink işlevi.</span><span class="sxs-lookup"><span data-stu-id="33cc0-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="33cc0-148">Gulp görev 20 iletileri IOT hub'ından Pi gönderir, her iki saniye LED blink görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="33cc0-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="33cc0-149">Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.</span><span class="sxs-lookup"><span data-stu-id="33cc0-149">The last one is a "stop" message that stops the application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="33cc0-151">Özet</span><span class="sxs-lookup"><span data-stu-id="33cc0-151">Summary</span></span>
<span data-ttu-id="33cc0-152">IOT hub'ından LED blink Pi için başarıyla iletileri gönderdik.</span><span class="sxs-lookup"><span data-stu-id="33cc0-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="33cc0-153">Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="33cc0-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33cc0-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33cc0-154">Next steps</span></span>
[<span data-ttu-id="33cc0-155">Açık ve kapalı LED davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="33cc0-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
