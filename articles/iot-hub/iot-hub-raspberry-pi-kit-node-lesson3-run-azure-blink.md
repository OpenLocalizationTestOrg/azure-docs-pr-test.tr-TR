---
title: "Azure IOT - Ders 3 Raspberry Pi'yi (düğüm) bağlanma: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve IOT hub'ına iletileri gönderir ve ışığı yanıp Raspberry Pi 3 örnek uygulamayı çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: blink bulut pi neden, buluttan blink neden
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="8908b-104">Cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8908b-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8908b-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="8908b-105">What you will do</span></span>
<span data-ttu-id="8908b-106">Bu makalede dağıtmak ve IOT hub'ına iletileri gönderir Raspberry Pi 3 örnek bir uygulamayı çalıştırmak nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8908b-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="8908b-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8908b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8908b-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="8908b-108">What you will learn</span></span>
<span data-ttu-id="8908b-109">Gulp aracı dağıtmak ve örnek Node.js uygulaması Pi üzerinde çalıştırmak için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8908b-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8908b-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8908b-110">What you need</span></span>
* <span data-ttu-id="8908b-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir depolama hesabı oluştur](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8908b-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="8908b-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="8908b-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="8908b-113">Cihaz bağlantı dizesi, Pi tarafından IOT hub'ınıza bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8908b-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="8908b-114">IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8908b-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="8908b-115">Kaynak grubunuzdaki tüm IOT hub aşağıdaki Azure CLI komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="8908b-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="8908b-116">Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="8908b-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="8908b-117">IOT hub bağlantı dizesine aşağıdaki Azure CLI komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="8908b-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="8908b-118">`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Pi kayıtlı belirtilen adıdır.</span><span class="sxs-lookup"><span data-stu-id="8908b-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="8908b-119">Cihaz bağlantı dizesi, aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="8908b-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="8908b-120">Kullanım `myraspberrypi` değeri olarak `{device id}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="8908b-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="8908b-121">Aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8908b-121">Configure the device connection</span></span>
1. <span data-ttu-id="8908b-122">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="8908b-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="8908b-123">Aygıt yapılandırma dosyasını açın `config-raspberrypi.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="8908b-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="8908b-125">İçinde aşağıdaki değişiklikleri yapın `config-raspberrypi.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="8908b-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="8908b-126">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** dan aldığınız cihaz IP adresi veya ana bilgisayar adı ile `device-discovery-cli` veya Cihazınızı yapılandırıldığında devralınan değere sahip.</span><span class="sxs-lookup"><span data-stu-id="8908b-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="8908b-127">Değiştir **[IOT cihaz bağlantı dizesi]** ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="8908b-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="8908b-128">Değiştir **[IOT hub bağlantı dizesine]** ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="8908b-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="8908b-129">Güncelleştirme `config-raspberrypi.json` bilgisayarınızdan örnek uygulama dağıtabilirsiniz, böylece dosya.</span><span class="sxs-lookup"><span data-stu-id="8908b-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8908b-130">Dağıtma ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8908b-130">Deploy and run the sample application</span></span>
<span data-ttu-id="8908b-131">Dağıtma ve aşağıdaki komutu çalıştırarak Pi üzerinde örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8908b-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="8908b-132">Örnek uygulama çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8908b-132">Verify that the sample application works</span></span>
<span data-ttu-id="8908b-133">Her iki saniye yanıp sönen Pi bağlı LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8908b-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="8908b-134">IŞIĞI yanıp her zaman, örnek uygulamayı IOT hub'ınıza ileti gönderir ve iletinin IOT hub'ınıza başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="8908b-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="8908b-135">Ayrıca, IOT hub tarafından alınan her ileti konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="8908b-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="8908b-136">Örnek uygulama, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="8908b-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="8908b-138">Özet</span><span class="sxs-lookup"><span data-stu-id="8908b-138">Summary</span></span>
<span data-ttu-id="8908b-139">Dağıtılan artık ve IOT hub'ına cihaz bulut iletilerini göndermek için Pi üzerinde yeni blink örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8908b-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="8908b-140">Depolama hesabına yazılan gibi iletilerinizi şimdi izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8908b-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8908b-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8908b-141">Next steps</span></span>
[<span data-ttu-id="8908b-142">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="8908b-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

