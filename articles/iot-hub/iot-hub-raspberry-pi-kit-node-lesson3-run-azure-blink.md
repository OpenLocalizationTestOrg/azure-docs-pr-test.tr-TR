---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: örneği çalıştırmak | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooRaspberry tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp Pi 3 çalıştırın."
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
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="0a047-104">Örnek uygulama toosend cihaz bulut iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0a047-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0a047-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="0a047-105">What you will do</span></span>
<span data-ttu-id="0a047-106">Bu makale size nasıl toodeploy ve gönderir Raspberry Pi 3 örnek bir uygulama çalıştırılmasında iletileri tooyour IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0a047-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="0a047-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0a047-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0a047-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="0a047-108">What you will learn</span></span>
<span data-ttu-id="0a047-109">Nasıl toouse hello aracı toodeploy gulp ve Merhaba örnek Node.js uygulaması Pi üzerinde çalıştırmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0a047-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0a047-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0a047-110">What you need</span></span>
* <span data-ttu-id="0a047-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="0a047-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="0a047-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="0a047-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="0a047-113">Merhaba cihaz bağlantı dizesi, Pi tooconnect tooyour IOT hub tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a047-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="0a047-114">Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="0a047-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="0a047-115">Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:</span><span class="sxs-lookup"><span data-stu-id="0a047-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="0a047-116">Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="0a047-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="0a047-117">Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:</span><span class="sxs-lookup"><span data-stu-id="0a047-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="0a047-118">`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Pi kayıtlı belirtilen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="0a047-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="0a047-119">Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="0a047-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="0a047-120">Kullanım `myraspberrypi` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="0a047-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="0a047-121">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0a047-121">Configure hello device connection</span></span>
1. <span data-ttu-id="0a047-122">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="0a047-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="0a047-123">Açık hello aygıt yapılandırma dosyası `config-raspberrypi.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="0a047-123">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="0a047-125">Merhaba değişikliklerini aşağıdaki hello olun `config-raspberrypi.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0a047-125">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="0a047-126">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** dan aldığınız hello aygıt IP adresi veya ana bilgisayar adı ile `device-discovery-cli` veya Cihazınızı yapılandırıldığında devralınan hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="0a047-126">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="0a047-127">Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="0a047-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="0a047-128">Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="0a047-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="0a047-129">Güncelleştirme hello `config-raspberrypi.json` Merhaba örnek uygulaması bilgisayarınızdan dağıtabilirsiniz dosyasını.</span><span class="sxs-lookup"><span data-stu-id="0a047-129">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="0a047-130">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0a047-130">Deploy and run hello sample application</span></span>
<span data-ttu-id="0a047-131">Dağıtma ve hello aşağıdaki komutu çalıştırarak Pi üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0a047-131">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="0a047-132">Merhaba örnek uygulaması çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0a047-132">Verify that hello sample application works</span></span>
<span data-ttu-id="0a047-133">Her iki saniye yanıp sönen bağlı tooPi olan hello LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a047-133">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="0a047-134">Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="0a047-134">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="0a047-135">Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="0a047-135">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="0a047-136">Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="0a047-136">hello sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="0a047-138">Özet</span><span class="sxs-lookup"><span data-stu-id="0a047-138">Summary</span></span>
<span data-ttu-id="0a047-139">Dağıtılan artık ve Pi toosend cihaz bulut iletilerini tooyour IOT hub'ına hello yeni blink örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0a047-139">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="0a047-140">Toohello depolama hesabı yazıldığı şekilde iletilerinizi şimdi izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a047-140">You can now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a047-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0a047-141">Next steps</span></span>
[<span data-ttu-id="0a047-142">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="0a047-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

