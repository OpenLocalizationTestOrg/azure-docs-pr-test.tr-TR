---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 3: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooRaspberry tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp Pi 3 çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: blink bulut pi neden, buluttan blink neden
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="f9fbe-104">Örnek uygulama toosend cihaz bulut iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f9fbe-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f9fbe-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="f9fbe-105">What you will do</span></span>
<span data-ttu-id="f9fbe-106">Bu makale size nasıl toodeploy ve gönderir Raspberry Pi 3 örnek bir uygulama çalıştırılmasında iletileri tooyour IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="f9fbe-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f9fbe-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f9fbe-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="f9fbe-108">What you will learn</span></span>
<span data-ttu-id="f9fbe-109">Nasıl toouse hello aracı toodeploy gulp ve Merhaba örnek Node.js uygulaması Pi üzerinde çalıştırmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f9fbe-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="f9fbe-110">What you need</span></span>
* <span data-ttu-id="f9fbe-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="f9fbe-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="f9fbe-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="f9fbe-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="f9fbe-113">Merhaba cihaz bağlantı dizesi, Pi tooconnect tooyour IOT hub tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="f9fbe-114">Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="f9fbe-115">Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="f9fbe-116">Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="f9fbe-117">Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="f9fbe-118">`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Pi kayıtlı belirtilen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="f9fbe-119">Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="f9fbe-120">Kullanım `myraspberrypi` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="f9fbe-121">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f9fbe-121">Configure hello device connection</span></span>
1. <span data-ttu-id="f9fbe-122">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="f9fbe-123">Çalıştırma **yükleme araçları gulp** yanı, Ders 1'de yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="f9fbe-124">Açık hello aygıt yapılandırma dosyası `config-raspberrypi.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="f9fbe-126">Merhaba değişikliklerini aşağıdaki hello olun `config-raspberrypi.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="f9fbe-127">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** dan aldığınız hello aygıt IP adresi veya ana bilgisayar adı ile `device-discovery-cli` veya Cihazınızı yapılandırıldığında devralınan hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="f9fbe-128">Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="f9fbe-129">Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="f9fbe-130">Gerekmeyen `azure_storage_connection_string` bu makalede.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="f9fbe-131">Olduğu gibi tutun.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-131">Keep it as is.</span></span>

<span data-ttu-id="f9fbe-132">Güncelleştirme hello `config-raspberrypi.json` Merhaba örnek uygulaması bilgisayarınızdan dağıtabilirsiniz dosyasını.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="f9fbe-133">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f9fbe-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="f9fbe-134">Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f9fbe-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="f9fbe-135">Merhaba örnek uygulaması çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f9fbe-135">Verify that hello sample application works</span></span>
<span data-ttu-id="f9fbe-136">Her iki saniye yanıp sönen bağlı tooPi olan hello LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="f9fbe-137">Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="f9fbe-138">Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="f9fbe-139">Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="f9fbe-141">Özet</span><span class="sxs-lookup"><span data-stu-id="f9fbe-141">Summary</span></span>
<span data-ttu-id="f9fbe-142">Dağıtılan artık ve Pi toosend cihaz bulut iletilerini tooyour IOT hub'ına hello yeni blink örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="f9fbe-143">Toohello depolama hesabı yazıldığı şekilde şimdi iletilerinizi izleyin.</span><span class="sxs-lookup"><span data-stu-id="f9fbe-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9fbe-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9fbe-144">Next steps</span></span>
[<span data-ttu-id="f9fbe-145">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="f9fbe-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

