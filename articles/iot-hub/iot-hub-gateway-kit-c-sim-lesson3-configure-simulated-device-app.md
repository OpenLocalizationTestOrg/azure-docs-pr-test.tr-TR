---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "IOT hub'ınıza sıcaklık veri göndermek için bir sanal cihaz örnek uygulamayı çalıştırma"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Bulut için veri"
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="b0738-104">Yapılandırma ve sanal cihaz örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b0738-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b0738-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="b0738-105">What you will do</span></span>

- <span data-ttu-id="b0738-106">Örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b0738-106">Clone the sample repository.</span></span>
- <span data-ttu-id="b0738-107">IOT hub ve sanal cihaz örnek uygulama için mantıksal aygıt bilgilerini almak için Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0738-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="b0738-108">Yapılandırın ve sanal cihaz örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0738-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="b0738-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b0738-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b0738-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="b0738-110">What you will learn</span></span>

<span data-ttu-id="b0738-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="b0738-111">In this article, you will learn:</span></span>

- <span data-ttu-id="b0738-112">Nasıl yapılandırmak ve sanal cihaz örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0738-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b0738-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="b0738-113">What you need</span></span>

<span data-ttu-id="b0738-114">Başarılı bir şekilde tamamladınız gerekir</span><span class="sxs-lookup"><span data-stu-id="b0738-114">You must have successfully completed</span></span>

- [<span data-ttu-id="b0738-115">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="b0738-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="b0738-116">Ana bilgisayara örnek depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="b0738-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="b0738-117">Örnek deposuna kopyalamak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b0738-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="b0738-118">Windows komut istemi veya terminal macOS veya Ubuntu açın.</span><span class="sxs-lookup"><span data-stu-id="b0738-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="b0738-119">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0738-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="b0738-120">Sanal cihazı ve, NUC yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b0738-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="b0738-121">Yapılandırma dosyasını açın `config.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="b0738-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="b0738-122">Değiştir `"has_sensortag": true` ile`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="b0738-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Config tı SensorTag cihaz yok](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="b0738-124">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="b0738-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="b0738-125">Açık `config-gateway.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="b0738-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="b0738-126">Aşağıdaki kod satırını bulun ve değiştirin `[device hostname or IP address]` Intel NUC IP adresi veya ana bilgisayar adına sahip.</span><span class="sxs-lookup"><span data-stu-id="b0738-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="b0738-127">![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="b0738-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="b0738-128">IOT hub mantıksal aygıtı bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="b0738-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="b0738-129">Mantıksal Cihazınızı Azure IOT hub bağlantı dizesini almak için ana bilgisayarda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0738-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="b0738-130">`{IoT hub name}`kullandığınız IOT hub addır.</span><span class="sxs-lookup"><span data-stu-id="b0738-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="b0738-131">IOT ağ geçidi değeri olarak kullanın `{resource group name}` ve mydevice değeri olarak `{device id}` Ders 2 değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="b0738-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="b0738-132">Sanal cihaz bulut karşıya yükleme örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0738-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="b0738-133">Yapılandırmak ve sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b0738-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="b0738-134">Açık `config-sensortag.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="b0738-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="b0738-136">Kod içinde aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="b0738-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="b0738-137">Değiştir `[IoT hub name]` IOT hub'ı adı ile.</span><span class="sxs-lookup"><span data-stu-id="b0738-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="b0738-138">Değiştir `[IoT device connection string]` IOT hub mantıksal aygıtı bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="b0738-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="b0738-139">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0738-139">Run the application.</span></span>

   <span data-ttu-id="b0738-140">Dağıtma ve aşağıdaki komutu çalıştırarak uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0738-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="b0738-141">Örnek uygulama çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="b0738-141">Verify the sample application works</span></span>

<span data-ttu-id="b0738-142">Şimdi aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b0738-142">You should now see output like the following:</span></span>

![Sanal cihaz örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="b0738-144">Uygulama için 40 saniye sürer, IOT hub ' ınızı sıcaklık verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="b0738-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="b0738-145">Özet</span><span class="sxs-lookup"><span data-stu-id="b0738-145">Summary</span></span>

<span data-ttu-id="b0738-146">Başarılı bir şekilde yapılandırılmış artık ve veri ile sanal cihaz IOT hub'ınıza gönderen sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0738-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0738-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0738-147">Next steps</span></span>
[<span data-ttu-id="b0738-148">IoT hub'ınızdan ileti okuma</span><span class="sxs-lookup"><span data-stu-id="b0738-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)