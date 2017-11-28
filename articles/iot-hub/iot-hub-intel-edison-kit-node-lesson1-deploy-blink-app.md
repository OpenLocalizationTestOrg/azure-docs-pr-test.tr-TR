---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 1 bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek C uygulaması github'dan kopyalayın ve bu uygulama tooyour Intel Edison'u Panosu gulp toodeploy çalıştırın. Bu örnek uygulama hello bağlı LED toohello Panosu her iki saniye yanıp."
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
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="76d91-105">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="76d91-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="76d91-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="76d91-106">What you will do</span></span>
<span data-ttu-id="76d91-107">Merhaba örnek C uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooIntel Edison'u kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d91-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="76d91-108">Merhaba örnek uygulaması, her iki saniye hello bağlı LED toohello Panosu yanıp.</span><span class="sxs-lookup"><span data-stu-id="76d91-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="76d91-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="76d91-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="76d91-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="76d91-110">What you will learn</span></span>
* <span data-ttu-id="76d91-111">Nasıl toodeploy ve çalışma hello Edison'u üzerinde örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="76d91-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="76d91-112">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="76d91-112">What you need</span></span>
<span data-ttu-id="76d91-113">Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="76d91-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="76d91-114">[Cihazınızı yapılandırın][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="76d91-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="76d91-115">[Merhaba araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="76d91-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="76d91-116">Açık Merhaba örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="76d91-116">Open hello sample application</span></span>
<span data-ttu-id="76d91-117">tooopen hello örnek uygulama, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="76d91-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="76d91-118">Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="76d91-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="76d91-119">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="76d91-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

<span data-ttu-id="76d91-121">Merhaba Hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="76d91-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="76d91-122">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="76d91-122">Install application dependencies</span></span>
<span data-ttu-id="76d91-123">Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="76d91-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="76d91-124">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="76d91-124">Configure hello device connection</span></span>
<span data-ttu-id="76d91-125">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="76d91-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="76d91-126">Hello aşağıdaki komutu çalıştırarak Hello aygıt yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="76d91-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="76d91-127">Merhaba yapılandırma dosyası `config-edison.json` içinde tooEdison toolog kullanmak hello kullanıcı kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="76d91-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="76d91-128">tooavoid hello sızıntısı kullanıcı kimlik bilgilerini, hello yapılandırma dosyası hello alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda hello giriş klasörünün.</span><span class="sxs-lookup"><span data-stu-id="76d91-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="76d91-129">Merhaba aygıt yapılandırma dosyasını Visual Studio kodda hello aşağıdaki komutu çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="76d91-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="76d91-130">Merhaba yer tutucu Değiştir `[device hostname or IP address]` ve `[device password]` başlangıç IP adresi ve içinde önceki Ders düşürüleceği parola.</span><span class="sxs-lookup"><span data-stu-id="76d91-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="76d91-132">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="76d91-132">Congratulations!</span></span> <span data-ttu-id="76d91-133">Merhaba ilk örnek bir uygulama için Edison'u başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="76d91-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="76d91-134">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="76d91-134">Deploy and run hello sample application</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="76d91-135">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="76d91-135">Deploy and run hello sample app</span></span>
<span data-ttu-id="76d91-136">Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76d91-136">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="76d91-137">Merhaba uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="76d91-137">Verify hello app works</span></span>
<span data-ttu-id="76d91-138">Merhaba örnek uygulama için 20 kez Hello ışığı yanıp sonra otomatik olarak sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="76d91-138">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="76d91-139">Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="76d91-139">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a><span data-ttu-id="76d91-141">Özet</span><span class="sxs-lookup"><span data-stu-id="76d91-141">Summary</span></span>
<span data-ttu-id="76d91-142">Gerekli hello araçları toowork ile Edison'u yüklü ve örnek uygulama tooEdison tooblink hello LED dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="76d91-142">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="76d91-143">Artık oluşturmak, dağıtmak ve Edison'u tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d91-143">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d91-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76d91-144">Next steps</span></span>
<span data-ttu-id="76d91-145">[Hello Azure Araçları edinin][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="76d91-145">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
