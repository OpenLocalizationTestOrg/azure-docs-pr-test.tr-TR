---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 3 bağlanın: ileti gönderme | Microsoft Docs"
description: "Dağıtma ve örnek uygulama tooIntel tooyour IOT hub'ı iletileri gönderir ve hello ışığı yanıp Edison'u çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT bulut hizmeti, arduino veri toocloud Gönder"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="abc0d-104">Örnek uygulama toosend cihaz bulut iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="abc0d-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="abc0d-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="abc0d-105">What you will do</span></span>
<span data-ttu-id="abc0d-106">Bu makale size nasıl toodeploy ve gönderir Intel Edison'u örnek bir uygulama çalıştırılmasında iletileri tooyour IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="abc0d-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="abc0d-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="abc0d-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="abc0d-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="abc0d-108">What you will learn</span></span>
<span data-ttu-id="abc0d-109">Siz nasıl toouse hello gulp aracı toodeploy öğrenin ve üzerinde Edison'u hello örnek C uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="abc0d-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="abc0d-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="abc0d-110">What you need</span></span>
* <span data-ttu-id="abc0d-111">Bu görev başlamadan önce başarılı bir şekilde tamamladınız gerekir [bir Azure işlevi uygulama ve bir depolama hesabı tooprocess deposu IOT hub ve iletileri oluşturmak][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="abc0d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="abc0d-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="abc0d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="abc0d-113">kullanılan tooconnect tooyour IOT hub'ı Edison'u Hello cihaz bağlantı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="abc0d-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="abc0d-114">IOT hub bağlantı dizesine hello kullanılan tooconnect Edison'u hello IOT hub'ı temsil eden, IOT hub toohello aygıt kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="abc0d-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="abc0d-115">Azure CLI komutu aşağıdaki hello çalıştırarak kaynak grubunuzdaki tüm IOT hub listesi:</span><span class="sxs-lookup"><span data-stu-id="abc0d-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="abc0d-116">Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="abc0d-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="abc0d-117">Azure CLI komutu aşağıdaki hello çalıştırarak Hello IOT hub bağlantı dizesine alın:</span><span class="sxs-lookup"><span data-stu-id="abc0d-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="abc0d-118">`{my hub name}`ne zaman IOT hub'ınızı oluşturduğunuz ve Edison'u kayıtlı belirtilen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="abc0d-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="abc0d-119">Merhaba cihaz bağlantı dizesi hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="abc0d-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="abc0d-120">Kullanım `myinteledison` hello değeri olarak `{device id}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="abc0d-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="abc0d-121">Merhaba aygıt bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="abc0d-121">Configure hello device connection</span></span>
1. <span data-ttu-id="abc0d-122">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="abc0d-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="abc0d-123">Açık hello aygıt yapılandırma dosyası `config-edison.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="abc0d-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="abc0d-125">Merhaba değişikliklerini aşağıdaki hello olun `config-edison.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="abc0d-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="abc0d-126">Değiştir **[aygıt ana bilgisayar adı veya IP adresi]** , düşürüleceği Cihazınızı yapılandırıldığında hello cihaz IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="abc0d-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="abc0d-127">Değiştir **[IOT cihaz bağlantı dizesi]** hello ile `device connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="abc0d-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="abc0d-128">Değiştir **[IOT hub bağlantı dizesine]** hello ile `iot hub connection string` , elde edilen.</span><span class="sxs-lookup"><span data-stu-id="abc0d-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="abc0d-129">Gerekmeyen `azure_storage_connection_string` bu makalede.</span><span class="sxs-lookup"><span data-stu-id="abc0d-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="abc0d-130">Olduğu gibi tutun.</span><span class="sxs-lookup"><span data-stu-id="abc0d-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="abc0d-131">Dağıtma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="abc0d-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="abc0d-132">Dağıtma ve hello aşağıdaki komutu çalıştırarak Edison'u üzerinde hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="abc0d-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="abc0d-133">Merhaba örnek uygulaması çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="abc0d-133">Verify that hello sample application works</span></span>
<span data-ttu-id="abc0d-134">Her iki saniye yanıp sönen bağlı tooEdison olan hello LED görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="abc0d-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="abc0d-135">Merhaba ışığı yanıp her zaman, Merhaba örnek uygulaması bir ileti tooyour IOT hub'ı gönderir ve o hello iletisi tooyour IOT hub'ı başarıyla gönderildi doğrular.</span><span class="sxs-lookup"><span data-stu-id="abc0d-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="abc0d-136">Ayrıca, hello IOT hub tarafından alınan her ileti hello konsol penceresinde yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="abc0d-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="abc0d-137">Merhaba örnek uygulaması, 20 ileti gönderdikten sonra otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="abc0d-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![Örnek uygulama ile gönderilen ve alınan iletileri][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="abc0d-139">Özet</span><span class="sxs-lookup"><span data-stu-id="abc0d-139">Summary</span></span>
<span data-ttu-id="abc0d-140">Dağıtılan artık ve hello yeni blink örnek uygulamayı Edison'u üzerinde toosend cihaz bulut iletilerini tooyour IOT hub'ı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="abc0d-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="abc0d-141">Toohello depolama hesabı yazıldığı şekilde şimdi iletilerinizi izleyin.</span><span class="sxs-lookup"><span data-stu-id="abc0d-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abc0d-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="abc0d-142">Next steps</span></span>
<span data-ttu-id="abc0d-143">[İletileri okuma Azure Depolama'da kalıcı][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="abc0d-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md