---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek Arduino uygulaması github'dan kopyalayın ve bu uygulama tooyour Adafruit yumuşatma M0 WiFi gulp toodeploy çalıştırın. Bu örnek uygulama hello GPIO'yu yanıp"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projeleri arduino neden, arduino öncülük blink, neden arduino blink kodunu arduino blink programı, arduino blink örneği"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="4ce10-105">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="4ce10-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4ce10-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="4ce10-106">What you will do</span></span>
<span data-ttu-id="4ce10-107">Merhaba örnek Arduino uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooyour Adafruit yumuşatma M0 WiFi Arduino Panosu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ce10-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="4ce10-108">Merhaba örnek uygulama yanıp sönme hello barod GPIO'yu #13 her iki saniye GEREKTİRİYORDU.</span><span class="sxs-lookup"><span data-stu-id="4ce10-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="4ce10-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="4ce10-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4ce10-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="4ce10-110">What you will learn</span></span>
* <span data-ttu-id="4ce10-111">Nasıl toodeploy ve çalışma hello Arduino panonuzu üzerinde örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="4ce10-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ce10-112">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="4ce10-112">What you need</span></span>
<span data-ttu-id="4ce10-113">Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ce10-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="4ce10-114">[Cihazınızı yapılandırın][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="4ce10-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="4ce10-115">[Merhaba araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="4ce10-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="4ce10-116">Açık Merhaba örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="4ce10-116">Open hello sample application</span></span>
<span data-ttu-id="4ce10-117">tooopen hello örnek uygulama, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce10-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="4ce10-118">Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="4ce10-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="4ce10-119">Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="4ce10-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

<span data-ttu-id="4ce10-121">Merhaba `app.ino` hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="4ce10-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="4ce10-122">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="4ce10-122">Install application dependencies</span></span>
<span data-ttu-id="4ce10-123">Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce10-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="4ce10-124">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4ce10-124">Configure hello device connection</span></span>
<span data-ttu-id="4ce10-125">tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce10-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="4ce10-126">Merhaba seri bağlantı noktası hello aygıt bulma CLI hello cihazının alın:</span><span class="sxs-lookup"><span data-stu-id="4ce10-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="4ce10-127">Toohello aşağıdadır benzer bir çıktı görmeniz ve hello usb Arduino panonuzu COM bağlantı noktasını Bul: ![aygıt bulma][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="4ce10-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="4ce10-128">Açık hello dosya `config.json` hello Ders klasörü ve COM bağlantı noktası numarası bulunan hello hello değerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce10-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="4ce10-130">Windows platformunda hello COM bağlantı noktası için hello biçimi olan `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="4ce10-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="4ce10-131">MacOS veya Ubuntu, ile başlayan `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="4ce10-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="4ce10-132">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4ce10-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="4ce10-133">Arduino panonuz için gerekli hello araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="4ce10-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="4ce10-134">Hello Azure IOT Hub SDK'sı Arduino panonuz için komutu aşağıdaki hello çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4ce10-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="4ce10-135">Bu görev, ağ bağlantınızın bağlı olarak bir uzun süre toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="4ce10-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="4ce10-136">Lütfen gulp görevler çalışırken Arduino IDE örneği hello çıkın: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="4ce10-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="4ce10-137">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4ce10-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="4ce10-138">Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4ce10-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="4ce10-139">Merhaba uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="4ce10-139">Verify hello app works</span></span>
<span data-ttu-id="4ce10-140">Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting-page] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="4ce10-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a><span data-ttu-id="4ce10-142">Özet</span><span class="sxs-lookup"><span data-stu-id="4ce10-142">Summary</span></span>
<span data-ttu-id="4ce10-143">Gerekli hello araçları toowork Arduino panonuzu yüklü ve bir örnek uygulama tooyour Arduino Panosu tooblink hello LED dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4ce10-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="4ce10-144">Artık oluşturmak, dağıtmak ve Arduino Panosu tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alacak.</span><span class="sxs-lookup"><span data-stu-id="4ce10-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ce10-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ce10-145">Next steps</span></span>
<span data-ttu-id="4ce10-146">[Hello Azure Araçları edinin][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="4ce10-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md