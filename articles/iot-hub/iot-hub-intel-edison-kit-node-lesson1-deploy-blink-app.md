---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: uygulama dağıtma | Microsoft Docs"
description: "Örnek C uygulama github'dan kopyalama ve Intel Edison'u panonuzu bu uygulamayı dağıtmak için gulp çalıştırın. Bu örnek uygulama panosuna her iki saniye bağlı ışığı yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projeleri arduino neden, arduino öncülük blink, neden arduino blink kodunu arduino blink programı, arduino blink örneği"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="e71a1-105">Blink uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="e71a1-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e71a1-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="e71a1-106">What you will do</span></span>
<span data-ttu-id="e71a1-107">Örnek C uygulama github'dan kopyalama ve Intel Edison'u örnek uygulamayı dağıtmak için gulp aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e71a1-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="e71a1-108">Örnek uygulama panosuna her iki saniye bağlı ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="e71a1-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="e71a1-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e71a1-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e71a1-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="e71a1-110">What you will learn</span></span>
* <span data-ttu-id="e71a1-111">Nasıl dağıtmak ve Edison'u üzerinde örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e71a1-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e71a1-112">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e71a1-112">What you need</span></span>
<span data-ttu-id="e71a1-113">Aşağıdaki işlemleri başarıyla tamamlandı gerekir:</span><span class="sxs-lookup"><span data-stu-id="e71a1-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="e71a1-114">[Cihazınızı yapılandırın][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="e71a1-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="e71a1-115">[Araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="e71a1-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="e71a1-116">Örnek uygulamayı Aç</span><span class="sxs-lookup"><span data-stu-id="e71a1-116">Open the sample application</span></span>
<span data-ttu-id="e71a1-117">Örnek uygulamayı açmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e71a1-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="e71a1-118">Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="e71a1-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="e71a1-119">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="e71a1-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

<span data-ttu-id="e71a1-121">Dosyada `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="e71a1-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e71a1-122">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="e71a1-122">Install application dependencies</span></span>
<span data-ttu-id="e71a1-123">Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e71a1-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="e71a1-124">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e71a1-124">Configure the device connection</span></span>
<span data-ttu-id="e71a1-125">Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e71a1-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="e71a1-126">Aşağıdaki komutu çalıştırarak aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e71a1-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="e71a1-127">Yapılandırma dosyası `config-edison.json` Edison'u için oturum açmak için kullandığınız kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e71a1-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="e71a1-128">Kullanıcı kimlik bilgilerini sızıntısını önlemek için yapılandırma dosyası alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="e71a1-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="e71a1-129">Aygıt yapılandırma dosyası, aşağıdaki komutu çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="e71a1-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="e71a1-130">Yer tutucu Değiştir `[device hostname or IP address]` ve `[device password]` içinde önceki Ders düşürüleceği parolanın ve IP adresi ile.</span><span class="sxs-lookup"><span data-stu-id="e71a1-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="e71a1-132">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="e71a1-132">Congratulations!</span></span> <span data-ttu-id="e71a1-133">İlk örnek uygulama Edison'u için başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e71a1-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e71a1-134">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e71a1-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="e71a1-135">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e71a1-135">Deploy and run the sample app</span></span>
<span data-ttu-id="e71a1-136">Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e71a1-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="e71a1-137">Uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="e71a1-137">Verify the app works</span></span>
<span data-ttu-id="e71a1-138">Örnek uygulama için 20 kez ışığı yanıp sonra otomatik olarak sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="e71a1-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="e71a1-139">IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="e71a1-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a><span data-ttu-id="e71a1-141">Özet</span><span class="sxs-lookup"><span data-stu-id="e71a1-141">Summary</span></span>
<span data-ttu-id="e71a1-142">Edison'u ile çalışmak için gerekli araçları yüklü ve ışığı yanıp sönen bir örnek uygulamanın Edison'u için dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e71a1-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="e71a1-143">Şimdi oluşturmanıza, dağıtmanıza ve Edison'u ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e71a1-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e71a1-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e71a1-144">Next steps</span></span>
<span data-ttu-id="e71a1-145">[Azure Araçları edinin][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="e71a1-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
