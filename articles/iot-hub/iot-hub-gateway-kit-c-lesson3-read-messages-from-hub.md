---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından ana bilgisayar tooread hello iletilerde çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a6c79-104">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="a6c79-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a6c79-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="a6c79-105">What you will do</span></span>

- <span data-ttu-id="a6c79-106">Örnek kod, IOT hub'ından bilgisayar tooread iletileri ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a6c79-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="a6c79-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a6c79-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a6c79-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="a6c79-108">What you will learn</span></span>

<span data-ttu-id="a6c79-109">Nasıl toouse hello aracı tooread IOT hub'ınızı iletilerden gulp.</span><span class="sxs-lookup"><span data-stu-id="a6c79-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6c79-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="a6c79-110">What you need</span></span>

- <span data-ttu-id="a6c79-111">Merhaba Ders 3'te başarıyla çalıştırıldığını bırak örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="a6c79-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="a6c79-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="a6c79-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="a6c79-113">Merhaba cihaz bağlantı dizesi, cihaz (tı SensorTag veya sanal cihaz) tooconnect tooyour IOT hub tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6c79-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="a6c79-114">Merhaba IOT hub bağlantı dizesine kullanılan tooconnect toohello kimlik tooyour IOT hub'ı tooconnect izin verilir, IOT hub toomanage hello cihazları kayıt defterinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6c79-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="a6c79-115">Kaynak grubunuzdaki tüm IOT hub hello aşağıdaki komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="a6c79-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="a6c79-116">Kullanım `iot-gateway` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="a6c79-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="a6c79-117">Hello IOT hub bağlantı dizesine hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="a6c79-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="a6c79-118">`{my hub name}`Ders 2'de belirtilen hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="a6c79-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="a6c79-119">Merhaba cihaz bağlantısı hello örnek kod için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a6c79-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="a6c79-120">Güncelleştirme hello aygıt yapılandırma dosyası `config-azure.json` böylece IOT hub'ından ana bilgisayarınızda iletileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="a6c79-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="a6c79-121">toodo Bu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a6c79-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="a6c79-122">Açık `config-azure.json` komutu bir konsol penceresinde aşağıdaki hello çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="a6c79-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="a6c79-123">Merhaba değişikliklerini aşağıdaki hello olun `config-azure.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="a6c79-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="a6c79-125">Değiştir `[IoT hub connection string]` hello aldığınız IOT hub bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="a6c79-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a6c79-126">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="a6c79-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="a6c79-127">TI SensorTag varsa, SensorTag üzerinde zaten açık emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6c79-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="a6c79-128">Merhaba ağ geçidi örnek uygulamayı çalıştırın ve IOT Hub tarafından komutu aşağıdaki hello iletilerini okuyun:</span><span class="sxs-lookup"><span data-stu-id="a6c79-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="a6c79-129">Merhaba komutu okuyan ve SensorTag veya sanal cihaz sıcaklık verileri paketleri ve hello ileti tooyour IOT hub'ı 2 saniyede gönderir hello bırak örnek uygulamayı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="a6c79-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="a6c79-130">Bir alt işlem tooreceive selamlama iletisine olarak çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="a6c79-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="a6c79-131">gönderilen ve alınan tüm hizmetlerde Anında hello aynı konsol penceresinde hello iletileri ana makine hello.</span><span class="sxs-lookup"><span data-stu-id="a6c79-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="a6c79-132">Merhaba örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="a6c79-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![BIRAK örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="a6c79-134">Özet</span><span class="sxs-lookup"><span data-stu-id="a6c79-134">Summary</span></span>

<span data-ttu-id="a6c79-135">IOT hub'ından iletileri bir örnek kodu tooread çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="a6c79-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="a6c79-136">Azure table storage'da depolanan hazır tooread karışılama iletileri demektir.</span><span class="sxs-lookup"><span data-stu-id="a6c79-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6c79-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6c79-137">Next steps</span></span>
[<span data-ttu-id="a6c79-138">Azure işlev uygulaması ve Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6c79-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


