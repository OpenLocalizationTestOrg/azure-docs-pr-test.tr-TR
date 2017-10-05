---
title: "Azure IOT - Ders 1 Arduino bağlanın: uygulama dağıtma | Microsoft Docs"
description: "GitHub örnek Arduino uygulamadan kopyalama ve Adafruit yumuşatma M0 WiFi bu uygulamayı dağıtmak için gulp çalıştırın. Bu örnek uygulama GPIO'yu yanıp"
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="e574b-105">Blink uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="e574b-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e574b-106">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="e574b-106">What you will do</span></span>
<span data-ttu-id="e574b-107">GitHub örnek Arduino uygulamadan kopyalama ve Adafruit yumuşatma M0 WiFi Arduino panonuzu örnek uygulamayı dağıtmak için gulp aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e574b-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="e574b-108">Örnek uygulama yanıp sönme GPIO'yu #13 üzerinde-barod her iki saniye GEREKTİRİYORDU.</span><span class="sxs-lookup"><span data-stu-id="e574b-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="e574b-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="e574b-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e574b-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="e574b-110">What you will learn</span></span>
* <span data-ttu-id="e574b-111">Nasıl dağıtmak ve Arduino Panonuzda örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e574b-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e574b-112">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e574b-112">What you need</span></span>
<span data-ttu-id="e574b-113">Aşağıdaki işlemleri başarıyla tamamlandı gerekir:</span><span class="sxs-lookup"><span data-stu-id="e574b-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="e574b-114">[Cihazınızı yapılandırın][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="e574b-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="e574b-115">[Araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="e574b-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="e574b-116">Örnek uygulamayı Aç</span><span class="sxs-lookup"><span data-stu-id="e574b-116">Open the sample application</span></span>
<span data-ttu-id="e574b-117">Örnek uygulamayı açmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e574b-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="e574b-118">Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="e574b-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="e574b-119">Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="e574b-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Depodaki yapısı][repo-structure]

<span data-ttu-id="e574b-121">`app.ino` Dosyasını `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="e574b-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e574b-122">Uygulama bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="e574b-122">Install application dependencies</span></span>
<span data-ttu-id="e574b-123">Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e574b-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="e574b-124">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e574b-124">Configure the device connection</span></span>
<span data-ttu-id="e574b-125">Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e574b-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="e574b-126">Aygıtın aygıt bulma CLI ile seri bağlantı noktası alın:</span><span class="sxs-lookup"><span data-stu-id="e574b-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="e574b-127">Usb Arduino panonuzu COM bağlantı noktasını bulun ve aşağıdakine benzer bir çıktı görmeniz gerekir: ![aygıt bulma][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="e574b-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="e574b-128">Dosyayı açmak `config.json` Ders klasöründe bulunan COM bağlantı noktası numarası değerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e574b-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="e574b-130">COM bağlantı noktası, Windows platformunda için biçimi olan `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="e574b-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="e574b-131">MacOS veya Ubuntu, ile başlayan `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="e574b-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e574b-132">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e574b-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="e574b-133">Arduino panonuz için gerekli Araçları'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="e574b-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="e574b-134">Aşağıdaki komutu çalıştırarak Arduino panonuz için Azure IOT Hub SDK'sını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e574b-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="e574b-135">Bu görev, ağ bağlantınızın bağlı olarak tamamlanması uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e574b-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="e574b-136">Lütfen çalışan Arduino IDE örneği gulp görevleri çalıştırılırken çıkın: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="e574b-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="e574b-137">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e574b-137">Deploy and run the sample app</span></span>
<span data-ttu-id="e574b-138">Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e574b-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="e574b-139">Uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="e574b-139">Verify the app works</span></span>
<span data-ttu-id="e574b-140">IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu] [ troubleshooting-page] yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="e574b-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![IŞIĞI yanıp sönen][led-blinking]

## <a name="summary"></a><span data-ttu-id="e574b-142">Özet</span><span class="sxs-lookup"><span data-stu-id="e574b-142">Summary</span></span>
<span data-ttu-id="e574b-143">Arduino panonuzu ile çalışmak için gerekli araçları yüklü ve ışığı yanıp sönen bir örnek uygulamanın Arduino panonuz için dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e574b-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="e574b-144">Şimdi oluşturmanıza, dağıtmanıza ve Arduino panonuzu ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e574b-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e574b-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e574b-145">Next steps</span></span>
<span data-ttu-id="e574b-146">[Azure Araçları edinin][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="e574b-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md