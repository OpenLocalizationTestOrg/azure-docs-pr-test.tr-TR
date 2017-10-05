---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: örnek uygulamayı çalıştırma | Microsoft Docs"
description: "BIRAK SensorTag ve IOT hub'ınızı ' ndan veri almaya bırak örnek uygulamayı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bırak uygulama, algılayıcı İzleyici uygulama, algılayıcı veri toplama, algılayıcılar, bulut için algılayıcı verilerini verileri"
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="f5c22-104">Yapılandırma ve bırak örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f5c22-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f5c22-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="f5c22-105">What you will do</span></span>

- <span data-ttu-id="f5c22-106">Örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="f5c22-107">SensorTag ve Intel NUC arasında bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="f5c22-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="f5c22-108">IOT hub ve silinmesini devre dışı bırak (Bluetooth düşük enerji) örnek uygulaması SensorTag bilgilerini almak için Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="f5c22-109">Yapılandırmak ve bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="f5c22-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f5c22-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f5c22-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="f5c22-111">What you will learn</span></span>

<span data-ttu-id="f5c22-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="f5c22-112">In this article, you will learn:</span></span>

- <span data-ttu-id="f5c22-113">Nasıl yapılandırmak ve bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5c22-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="f5c22-114">What you need</span></span>

<span data-ttu-id="f5c22-115">Başarılı bir şekilde tamamladınız gerekir</span><span class="sxs-lookup"><span data-stu-id="f5c22-115">You must have successfully completed</span></span>

- [<span data-ttu-id="f5c22-116">IOT hub'ı oluşturma ve SensorTag kaydetme</span><span class="sxs-lookup"><span data-stu-id="f5c22-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="f5c22-117">Ana bilgisayara örnek depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="f5c22-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="f5c22-118">Örnek deposuna kopyalamak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f5c22-119">Windows komut istemi penceresi açın veya terminal macOS veya Ubuntu açın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="f5c22-120">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f5c22-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="f5c22-121">SensorTag ve Intel NUC arasında bağlantılar kurmak</span><span class="sxs-lookup"><span data-stu-id="f5c22-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="f5c22-122">Bağlantı kurmak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f5c22-123">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="f5c22-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="f5c22-124">Açık `config-gateway.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="f5c22-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="f5c22-125">Aşağıdaki kod satırını bulun ve değiştirin `[device hostname or IP address]` Intel NUC IP adresi veya ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="f5c22-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="f5c22-126">![config ağ geçidinin ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="f5c22-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="f5c22-127">Yardımcı Araçlar, aşağıdaki komutu çalıştırarak üzerinde Intel NUC yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="f5c22-128">Aşağıdaki resim olarak güç düğmesine basarak üzerinde SensorTag açın ve yeşil LED blink.</span><span class="sxs-lookup"><span data-stu-id="f5c22-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![Algılayıcı etiketi Aç](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="f5c22-130">Aşağıdaki komutları çalıştırarak SensorTag aygıtlarını tara:</span><span class="sxs-lookup"><span data-stu-id="f5c22-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="f5c22-131">Aşağıdaki komutu çalıştırarak SensorTag ve Intel NUC arasındaki bağlantıyı test edin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="f5c22-132">Değiştir `{mac address}` önceki adımda elde ettiğiniz MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="f5c22-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="f5c22-133">SensorTag bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="f5c22-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="f5c22-134">SensorTag Azure IOT hub bağlantı dizesini almak için ana bilgisayarda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f5c22-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="f5c22-135">`{IoT hub name}`kullandığınız IOT hub addır.</span><span class="sxs-lookup"><span data-stu-id="f5c22-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="f5c22-136">IOT ağ geçidi değeri olarak kullanın `{resource group name}` ve mydevice değeri olarak `{device id}` Ders 2 değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="f5c22-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="f5c22-137">BIRAK örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5c22-137">Configure the BLE sample application</span></span>

<span data-ttu-id="f5c22-138">Yapılandırmak ve bırak örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f5c22-139">Açık `config-sensortag.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="f5c22-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![config sensortag ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="f5c22-141">Kod içinde aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="f5c22-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="f5c22-142">Değiştir `[IoT hub name]` ile kullandığınız IOT hub adı.</span><span class="sxs-lookup"><span data-stu-id="f5c22-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="f5c22-143">Değiştir `[IoT device connection string]` aldığınız SensorTag bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="f5c22-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="f5c22-144">Değiştir `[device_mac_address]` aldığınız SensorTag MAC adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="f5c22-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="f5c22-145">BIRAK örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="f5c22-146">BIRAK örnek uygulamayı çalıştırmak için ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f5c22-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="f5c22-147">Üzerinde SensorTag açın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="f5c22-148">Dağıtma ve aşağıdaki komutu çalıştırarak üzerinde Intel NUC bırak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f5c22-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="f5c22-149">BIRAK örnek uygulama çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f5c22-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="f5c22-150">Şimdi, aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5c22-150">You should now see an output like the following:</span></span>

![BIRAK örnek uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="f5c22-152">Örnek uygulama sıcaklık veri toplamayı tutar ve IOT hub'ınıza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f5c22-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="f5c22-153">Örnek uygulama, 40 saniye gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="f5c22-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="f5c22-154">Özet</span><span class="sxs-lookup"><span data-stu-id="f5c22-154">Summary</span></span>

<span data-ttu-id="f5c22-155">Başarılı bir şekilde SensorTag ve Intel NUC arasında bağlantılar kurmak ve toplar ve veri SensorTag IOT hub'ınıza gönderir bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f5c22-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="f5c22-156">IOT hub'ınızı veri aldığını doğrulamak öğrenmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f5c22-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c22-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5c22-157">Next steps</span></span>
[<span data-ttu-id="f5c22-158">IoT hub'ınızdan ileti okuma</span><span class="sxs-lookup"><span data-stu-id="f5c22-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)