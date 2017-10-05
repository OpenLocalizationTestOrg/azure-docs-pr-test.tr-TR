---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
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
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="39c18-104">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="39c18-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="39c18-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="39c18-105">What you will do</span></span>

- <span data-ttu-id="39c18-106">Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39c18-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="39c18-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="39c18-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="39c18-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="39c18-108">What you will learn</span></span>

<span data-ttu-id="39c18-109">Gulp aracı IOT hub'ından iletileri okumak için nasıl kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39c18-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="39c18-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="39c18-110">What you need</span></span>

- <span data-ttu-id="39c18-111">Ders 3'te başarıyla çalıştırıldığını bırak örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="39c18-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="39c18-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="39c18-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="39c18-113">Cihaz bağlantı dizesi (tı SensorTag veya sanal cihaz) IOT hub'ınıza bağlanmak için aygıt tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39c18-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="39c18-114">IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39c18-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="39c18-115">Kaynak grubunuzdaki tüm IOT hub aşağıdaki komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="39c18-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="39c18-116">Kullanım `iot-gateway` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="39c18-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="39c18-117">IOT hub bağlantı dizesine, aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="39c18-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="39c18-118">`{my hub name}`Ders 2'de belirtilen adıdır.</span><span class="sxs-lookup"><span data-stu-id="39c18-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="39c18-119">Örnek kod için cihaz bağlantısı</span><span class="sxs-lookup"><span data-stu-id="39c18-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="39c18-120">Aygıt yapılandırma dosyasını güncelleştirme `config-azure.json` böylece IOT hub'ından ana bilgisayarınızda iletileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="39c18-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="39c18-121">Bunu yapmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="39c18-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="39c18-122">Açık `config-azure.json` Visual Studio konsol penceresinde aşağıdaki komutu çalıştırarak kod:</span><span class="sxs-lookup"><span data-stu-id="39c18-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="39c18-123">İçinde aşağıdaki değişiklikleri yapın `config-azure.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="39c18-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="39c18-125">Değiştir `[IoT hub connection string]` aldığınız IOT hub bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="39c18-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="39c18-126">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="39c18-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="39c18-127">TI SensorTag varsa, SensorTag üzerinde zaten açık emin olun.</span><span class="sxs-lookup"><span data-stu-id="39c18-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="39c18-128">Ağ geçidi örnek uygulamayı çalıştırın ve IOT Hub aşağıdaki komutla iletilerini okuyun:</span><span class="sxs-lookup"><span data-stu-id="39c18-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="39c18-129">Komutu okuyan ve SensorTag veya sanal cihaz sıcaklık verileri paketleri ve iletiyi 2 saniyede IOT hub'ınıza gönderir bırak örnek uygulamayı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="39c18-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="39c18-130">İleti almak için bir alt işlem olarak çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="39c18-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="39c18-131">Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="39c18-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="39c18-132">Örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="39c18-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![BIRAK örnek uygulama ile gönderilen ve alınan iletileri](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="39c18-134">Özet</span><span class="sxs-lookup"><span data-stu-id="39c18-134">Summary</span></span>

<span data-ttu-id="39c18-135">IOT hub'ından iletileri okumak için örnek kod çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="39c18-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="39c18-136">Azure table storage'da depolanan iletileri okumak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="39c18-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c18-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39c18-137">Next steps</span></span>
[<span data-ttu-id="39c18-138">Azure işlev uygulaması ve Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="39c18-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


