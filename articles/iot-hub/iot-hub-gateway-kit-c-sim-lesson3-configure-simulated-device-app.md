---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "Bir sanal cihaz örnek uygulama toosend sıcaklık veri tooyour IOT hub çalıştırın"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Veri toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="1c7ca-104">Yapılandırma ve sanal cihaz örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1c7ca-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="1c7ca-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="1c7ca-105">What you will do</span></span>

- <span data-ttu-id="1c7ca-106">Kopya hello örnek depo.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="1c7ca-107">Hello Azure CLI tooget sanal cihaz örnek bir uygulama için IOT hub ve mantıksal aygıt bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="1c7ca-108">Yapılandırma ve benzetimli hello aygıt örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="1c7ca-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1c7ca-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1c7ca-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="1c7ca-110">What you will learn</span></span>

<span data-ttu-id="1c7ca-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-111">In this article, you will learn:</span></span>

- <span data-ttu-id="1c7ca-112">Nasıl tooconfigure ve çalışma hello aygıt örnek uygulama benzetimi.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1c7ca-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="1c7ca-113">What you need</span></span>

<span data-ttu-id="1c7ca-114">Başarılı bir şekilde tamamladınız gerekir</span><span class="sxs-lookup"><span data-stu-id="1c7ca-114">You must have successfully completed</span></span>

- [<span data-ttu-id="1c7ca-115">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="1c7ca-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="1c7ca-116">Kopya hello örnek depo toohello ana bilgisayarı</span><span class="sxs-lookup"><span data-stu-id="1c7ca-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="1c7ca-117">tooclone hello örnek deposu, hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="1c7ca-118">Windows komut istemi veya terminal macOS veya Ubuntu açın.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="1c7ca-119">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="1c7ca-120">Merhaba sanal cihazı ve, NUC yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1c7ca-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="1c7ca-121">Açık hello yapılandırma dosyası `config.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="1c7ca-122">Değiştir `"has_sensortag": true` ile`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="1c7ca-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Config tı SensorTag cihaz yok](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="1c7ca-124">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="1c7ca-125">Açık `config-gateway.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="1c7ca-126">Aşağıdaki kod hello bulun ve değiştirin `[device hostname or IP address]` hello Intel NUC IP adresi veya ana bilgisayar adına sahip.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="1c7ca-127">![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="1c7ca-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="1c7ca-128">IOT hub mantıksal aygıtı Hello bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="1c7ca-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="1c7ca-129">tooget hello Azure IOT hub bağlantı dizesine hello ana bilgisayarda komut aşağıdaki hello çalıştırmak aygıtınızın mantıksal:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="1c7ca-130">`{IoT hub name}`kullandığınız hello IOT hub adıdır.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="1c7ca-131">IOT ağ geçidi hello değeri olarak kullanın `{resource group name}` ve mydevice hello değeri olarak `{device id}` Ders 2 hello değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="1c7ca-132">Benzetimli hello cihaz bulut karşıya yükleme örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1c7ca-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="1c7ca-133">tooconfigure ve benzetimli çalışma hello cihaz bulut örnek uygulamayı karşıya yüklemek, hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="1c7ca-134">Açık `config-sensortag.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="1c7ca-136">Merhaba kodda değişiklik aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="1c7ca-137">Değiştir `[IoT hub name]` hello IOT hub'ı adı ile.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="1c7ca-138">Değiştir `[IoT device connection string]` IOT hub'ı mantıksal aygıtınızın hello bağlantı dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="1c7ca-139">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-139">Run hello application.</span></span>

   <span data-ttu-id="1c7ca-140">Dağıtma ve hello aşağıdaki komutu çalıştırarak hello uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="1c7ca-141">Merhaba örnek uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="1c7ca-141">Verify hello sample application works</span></span>

<span data-ttu-id="1c7ca-142">Şimdi hello aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c7ca-142">You should now see output like hello following:</span></span>

![Sanal cihaz örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="1c7ca-144">Merhaba uygulaması, 40 saniye sürer sıcaklık veri tooyour IOT hub'ına gönderir.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="1c7ca-145">Özet</span><span class="sxs-lookup"><span data-stu-id="1c7ca-145">Summary</span></span>

<span data-ttu-id="1c7ca-146">Başarılı bir şekilde yapılandırdıysanız ve veri tooyour IOT hub ile sanal cihaz gönderen cihaz bulut karşıya yükleme örnek uygulamayı çalıştırma hello benzetimli.</span><span class="sxs-lookup"><span data-stu-id="1c7ca-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c7ca-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c7ca-147">Next steps</span></span>
[<span data-ttu-id="1c7ca-148">IoT hub'ınızdan ileti okuma</span><span class="sxs-lookup"><span data-stu-id="1c7ca-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)