---
title: "Azure IOT - Ders 4 Intel Edison'u (düğüm) bağlanma: iletileri alacak | Microsoft Docs"
description: "Örnek bir uygulama Edison'u üzerinde çalışır ve IOT hub'ınızı gelen iletilere izler. Yeni bir gulp görev iletileri için Edison'u LED blink için IOT hub'gönderir."
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
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="fa066-105">Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="fa066-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="fa066-106">Bu makalede, Intel Edison'u üzerinde örnek bir uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fa066-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="fa066-107">Örnek uygulama IOT hub'ınızı gelen iletilere izler.</span><span class="sxs-lookup"><span data-stu-id="fa066-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="fa066-108">Ayrıca Edison'u için IOT hub'ından iletileri göndermek için bilgisayarınızda gulp görevini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fa066-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="fa066-109">Örnek uygulama iletileri aldığında ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="fa066-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="fa066-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fa066-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fa066-111">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="fa066-111">What you will do</span></span>
* <span data-ttu-id="fa066-112">Örnek uygulama IOT hub'ınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fa066-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="fa066-113">Dağıtma ve örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fa066-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="fa066-114">İletileri LED blink Edison'u için IOT hub'ından gönderin.</span><span class="sxs-lookup"><span data-stu-id="fa066-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fa066-115">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="fa066-115">What you will learn</span></span>
<span data-ttu-id="fa066-116">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="fa066-116">In this article, you will learn:</span></span>
* <span data-ttu-id="fa066-117">IOT hub'ınızı gelen iletilere izlemek nasıl.</span><span class="sxs-lookup"><span data-stu-id="fa066-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="fa066-118">Edison'u için IOT hub'ından bulut-cihaz iletilerini göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="fa066-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fa066-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="fa066-119">What you need</span></span>
* <span data-ttu-id="fa066-120">Intel Edison'u ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa066-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="fa066-121">Edison'u ayarlama hakkında bilgi edinmek için bkz: [Cihazınızı yapılandırmak][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="fa066-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="fa066-122">Azure aboneliğinizde oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="fa066-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="fa066-123">IOT hub'ınızı oluşturmayı öğrenmek için bkz: [Azure IOT Hub'ınızı oluşturması][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="fa066-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="fa066-124">Örnek uygulama IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="fa066-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="fa066-125">Depodaki klasöründe olduğunuzdan emin olun `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="fa066-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="fa066-126">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="fa066-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="fa066-127">Dosyada `app` alt IOT hub'ından gelen iletileri izlemek için kod içeren anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="fa066-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="fa066-128">`blinkLED` İşlevi yanıp LED.</span><span class="sxs-lookup"><span data-stu-id="fa066-128">The `blinkLED` function blinks the LED.</span></span>

   ![Depodaki yapısında örnek uygulama][repo-structure]
2. <span data-ttu-id="fa066-130">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="fa066-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="fa066-131">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] dağıtma ve örnek uygulama çalıştırılıyor görev adımı atlayabilirsiniz bu bilgisayarda tüm yapılandırmaları, devralınır.</span><span class="sxs-lookup"><span data-stu-id="fa066-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="fa066-132">' Ndaki adımları tamamladıysanız [bir Azure işlevi uygulama ve depolama hesabı oluşturmayı] [ create-an-azure-function-app-and-storage-account] yer tutucuları değiştirmek gereken başka bir bilgisayara `config-edison.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="fa066-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="fa066-133">`config-edison.json` Giriş klasörü alt klasöründe bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="fa066-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Config edison.json dosyasının içeriği](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="fa066-135">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında aygıt IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="fa066-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="fa066-136">Değiştir **[IOT cihaz bağlantı dizesi]** çalıştırarak aldığınız cihaz bağlantı dizesiyle `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` komutu.</span><span class="sxs-lookup"><span data-stu-id="fa066-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="fa066-137">Değiştir **[IOT hub bağlantı dizesine]** çalıştırarak aldığınız IOT hub bağlantı dizesine sahip `az iot hub show-connection-string --name {my hub name}` komutu.</span><span class="sxs-lookup"><span data-stu-id="fa066-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="fa066-138">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fa066-138">Deploy and run the sample application</span></span>
<span data-ttu-id="fa066-139">Dağıtma ve aşağıdaki komutları çalıştırarak Edison'u üzerinde örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fa066-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="fa066-140">Gulp komutu Edison'u örnek uygulamayı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="fa066-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="fa066-141">Ardından, IOT hub'ından Edison'u için 20 blink iletileri göndermek için Edison'u ve ana bilgisayarınızda ayrı bir görev uygulama çalışır.</span><span class="sxs-lookup"><span data-stu-id="fa066-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="fa066-142">Örnek uygulama çalıştıktan sonra IOT hub'ından iletileri dinlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="fa066-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="fa066-143">Bu sırada, gulp görev Edison'u için IOT hub'ından birkaç "blink" iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="fa066-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="fa066-144">Örnek uygulama Edison'u alan her blink ileti için çağırır `blinkLED` LED blink işlevi.</span><span class="sxs-lookup"><span data-stu-id="fa066-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="fa066-145">Gulp görev 20 iletileri IOT hub'ından için Edison'u gönderir, her iki saniye LED blink görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa066-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="fa066-146">Bir uygulamanın çalışmasını durduran bir "Durdur" bir iletidir.</span><span class="sxs-lookup"><span data-stu-id="fa066-146">The last one is a "stop" message that stops the application from running.</span></span>

![Örnek uygulama ile komut gulp ve iletileri blink][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="fa066-148">Özet</span><span class="sxs-lookup"><span data-stu-id="fa066-148">Summary</span></span>
<span data-ttu-id="fa066-149">IOT hub'ından LED blink Edison'u için başarıyla iletileri gönderdik.</span><span class="sxs-lookup"><span data-stu-id="fa066-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="fa066-150">Sonraki görev isteğe bağlıdır: açık ve kapalı LED davranışını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa066-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa066-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa066-151">Next steps</span></span>
<span data-ttu-id="fa066-152">[Açık ve kapalı LED davranışını değiştirme][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="fa066-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md