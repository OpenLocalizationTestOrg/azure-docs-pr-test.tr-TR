---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından ana bilgisayar tooread hello iletilerde çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="e6b37-104">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="e6b37-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e6b37-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="e6b37-105">What you will do</span></span>

- <span data-ttu-id="e6b37-106">Örnek kod, IOT hub'ından bilgisayar tooread iletileri ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6b37-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="e6b37-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e6b37-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e6b37-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="e6b37-108">What you will learn</span></span>

<span data-ttu-id="e6b37-109">Nasıl toouse hello aracı tooread IOT hub'ınızı iletilerden gulp.</span><span class="sxs-lookup"><span data-stu-id="e6b37-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e6b37-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e6b37-110">What you need</span></span>

- <span data-ttu-id="e6b37-111">Merhaba sanal cihaz örnek [yapılandırma ve çalıştırma sanal cihaz bulut karşıya örnek uygulama](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="e6b37-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="e6b37-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="e6b37-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="e6b37-113">Merhaba cihaz bağlantı dizesi, sanal cihaz tooconnect tooyour IOT hub tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6b37-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="e6b37-114">Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6b37-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="e6b37-115">Kaynak grubunuzdaki tüm IOT hub hello aşağıdaki komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="e6b37-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="e6b37-116">Kullanım `iot-gateway` hello değeri olarak `{resource group name}` onu değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="e6b37-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="e6b37-117">Hello IOT hub bağlantı dizesine hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="e6b37-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="e6b37-118">`{my hub name}`Ders 2'de belirtilen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="e6b37-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="e6b37-119">Merhaba cihaz bağlantısı hello örnek kod için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6b37-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="e6b37-120">IOT hub ve cihaz bağlantısı yapılandırmalarını güncelleştirme `config-azure.json` hello aşağıdaki adımları gerçekleştirerek:</span><span class="sxs-lookup"><span data-stu-id="e6b37-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="e6b37-121">Açık `config-azure.json` komutu bir konsol penceresinde aşağıdaki hello çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="e6b37-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="e6b37-122">Merhaba değişikliklerini aşağıdaki hello olun `config-azure.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="e6b37-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="e6b37-124">Değiştir `[IoT hub connection string]` hello IOT hub bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="e6b37-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="e6b37-125">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="e6b37-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="e6b37-126">Benzetimli hello aygıt örnek uygulamayı çalıştırın ve IOT Hub tarafından komutu aşağıdaki hello iletilerini okuyun:</span><span class="sxs-lookup"><span data-stu-id="e6b37-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="e6b37-127">Merhaba komutu 2 saniyede tooyour IOT hub'ı iletileri gönderir Merhaba uygulaması çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e6b37-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="e6b37-128">Bir alt işlem tooreceive selamlama iletisine olarak çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="e6b37-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="e6b37-129">gönderilen ve alınan tüm hizmetlerde Anında hello aynı konsol penceresinde hello iletileri ana makine hello.</span><span class="sxs-lookup"><span data-stu-id="e6b37-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="e6b37-130">Merhaba uygulaması 40 saniye cinsinden çıkılacak.</span><span class="sxs-lookup"><span data-stu-id="e6b37-130">hello application will exit in 40 seconds.</span></span>

![Gönderilen ve alınan ileti ile sanal örnek uygulama](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="e6b37-132">Özet</span><span class="sxs-lookup"><span data-stu-id="e6b37-132">Summary</span></span>

<span data-ttu-id="e6b37-133">Sanal cihaz ile Merhaba örnek uygulama toosend veri tooyour IOT hub'ı başarıyla çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="e6b37-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="e6b37-134">Ayrıca tooyour IOT hub gönderilen Merhaba iletileri okuduğunuz.</span><span class="sxs-lookup"><span data-stu-id="e6b37-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6b37-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6b37-135">Next steps</span></span>
[<span data-ttu-id="e6b37-136">Azure işlev uygulaması ve Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6b37-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


