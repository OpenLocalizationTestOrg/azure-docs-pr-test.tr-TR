---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "BIRAK örnek uygulama tooreceive veri BOŞALT SensorTag ve IOT hub'ınızı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bırak uygulama, algılayıcı İzleyici uygulama, algılayıcı veri toplama, algılayıcılar, algılayıcı verileri toocloud verileri"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="466bf-104">Yapılandırma ve bırak örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="466bf-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="466bf-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="466bf-105">What you will do</span></span>

- <span data-ttu-id="466bf-106">Kopya hello örnek depo.</span><span class="sxs-lookup"><span data-stu-id="466bf-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="466bf-107">SensorTag ve Intel NUC arasında hello bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="466bf-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="466bf-108">Hello Azure CLI tooget bırak (Bluetooth düşük enerji) örnek bir uygulama için IOT hub ve SensorTag bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="466bf-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="466bf-109">Yapılandırmak ve hello bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="466bf-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="466bf-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="466bf-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="466bf-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="466bf-111">What you will learn</span></span>

<span data-ttu-id="466bf-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="466bf-112">In this article, you will learn:</span></span>

- <span data-ttu-id="466bf-113">Nasıl tooconfigure ve çalışma hello bırak örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="466bf-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="466bf-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="466bf-114">What you need</span></span>

<span data-ttu-id="466bf-115">Başarılı bir şekilde tamamladınız gerekir</span><span class="sxs-lookup"><span data-stu-id="466bf-115">You must have successfully completed</span></span>

- [<span data-ttu-id="466bf-116">IOT hub'ı oluşturma ve SensorTag kaydetme</span><span class="sxs-lookup"><span data-stu-id="466bf-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="466bf-117">Kopya hello örnek depo toohello ana bilgisayarı</span><span class="sxs-lookup"><span data-stu-id="466bf-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="466bf-118">tooclone hello örnek deposu, hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="466bf-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="466bf-119">Windows komut istemi penceresi açın veya terminal macOS veya Ubuntu açın.</span><span class="sxs-lookup"><span data-stu-id="466bf-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="466bf-120">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="466bf-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="466bf-121">SensorTag ve Intel NUC arasında hello bağlantısı ayarlama</span><span class="sxs-lookup"><span data-stu-id="466bf-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="466bf-122">Merhaba bağlantı kurma tooset hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="466bf-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="466bf-123">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="466bf-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="466bf-124">Açık `config-gateway.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="466bf-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="466bf-125">Aşağıdaki kod hello bulun ve değiştirin `[device hostname or IP address]` başlangıç IP adresi veya ana bilgisayar adı ile Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="466bf-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="466bf-126">![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="466bf-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="466bf-127">Yardımcı Araçlar hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC yükleyin:</span><span class="sxs-lookup"><span data-stu-id="466bf-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="466bf-128">Resim aşağıdaki hello hello güç düğmesine basarak üzerinde SensorTag açın ve hello yeşil LED blink.</span><span class="sxs-lookup"><span data-stu-id="466bf-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![Algılayıcı etiketi Aç](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="466bf-130">Merhaba aşağıdaki komutları çalıştırarak SensorTag aygıtlarını tara:</span><span class="sxs-lookup"><span data-stu-id="466bf-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="466bf-131">Merhaba SensorTag ve Intel NUC arasında Hello bağlantısı hello aşağıdaki komutu çalıştırarak test edin:</span><span class="sxs-lookup"><span data-stu-id="466bf-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="466bf-132">Değiştir `{mac address}` hello hello önceki adımda elde ettiğiniz MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="466bf-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="466bf-133">SensorTag Hello bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="466bf-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="466bf-134">tooget hello Azure IOT hub bağlantı dizesi SensorTag, komut hello ana bilgisayarda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="466bf-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="466bf-135">`{IoT hub name}`kullandığınız hello IOT hub adıdır.</span><span class="sxs-lookup"><span data-stu-id="466bf-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="466bf-136">IOT ağ geçidi hello değeri olarak kullanın `{resource group name}` ve mydevice hello değeri olarak `{device id}` Ders 2 hello değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="466bf-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="466bf-137">Merhaba bırak örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="466bf-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="466bf-138">tooconfigure ve çalışma hello bırak örnek uygulama, hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="466bf-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="466bf-139">Açık `config-sensortag.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="466bf-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="466bf-141">Merhaba kodda değişiklik aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="466bf-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="466bf-142">Değiştir `[IoT hub name]` kullandığınız hello IOT hub'ı adı ile.</span><span class="sxs-lookup"><span data-stu-id="466bf-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="466bf-143">Değiştir `[IoT device connection string]` aldığınız SensorTag hello bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="466bf-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="466bf-144">Değiştir `[device_mac_address]` hello hello aldığınız SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="466bf-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="466bf-145">Merhaba bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="466bf-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="466bf-146">toorun hello bırak örnek uygulama, hello ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="466bf-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="466bf-147">Üzerinde SensorTag açın.</span><span class="sxs-lookup"><span data-stu-id="466bf-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="466bf-148">Dağıtma ve hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC hello bırak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="466bf-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="466bf-149">Merhaba bırak örnek uygulaması çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="466bf-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="466bf-150">Şimdi hello aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="466bf-150">You should now see an output like hello following:</span></span>

![BIRAK örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="466bf-152">Merhaba örnek uygulaması sıcaklık veri toplamayı tutar ve tooyour IOT hub'ı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="466bf-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="466bf-153">Merhaba örnek uygulaması, 40 saniye gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="466bf-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="466bf-154">Özet</span><span class="sxs-lookup"><span data-stu-id="466bf-154">Summary</span></span>

<span data-ttu-id="466bf-155">Başarılı bir şekilde SensorTag ve Intel NUC arasında hello bağlantılar kurmak ve toplar ve SensorTag tooyour IOT hub'ından veri gönderen bir bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="466bf-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="466bf-156">Hazır toolearn olduğunuz nasıl IOT hub'ınızı aldı tooverify hello veri.</span><span class="sxs-lookup"><span data-stu-id="466bf-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="466bf-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="466bf-157">Next steps</span></span>
[<span data-ttu-id="466bf-158">IoT hub'ınızdan ileti okuma</span><span class="sxs-lookup"><span data-stu-id="466bf-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)