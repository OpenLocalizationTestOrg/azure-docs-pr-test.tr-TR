---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 3: iletileri okumak | Microsoft Docs"
description: "Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="cac77-104">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="cac77-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cac77-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="cac77-105">What you will do</span></span>

- <span data-ttu-id="cac77-106">Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cac77-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="cac77-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cac77-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cac77-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="cac77-108">What you will learn</span></span>

<span data-ttu-id="cac77-109">Gulp aracı IOT hub'ından iletileri okumak için nasıl kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cac77-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cac77-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="cac77-110">What you need</span></span>

- <span data-ttu-id="cac77-111">Sanal cihaz örnek [yapılandırma ve çalıştırma sanal cihaz bulut karşıya örnek uygulama](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="cac77-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="cac77-112">IOT hub ve cihaz bağlantı dizeleri alma</span><span class="sxs-lookup"><span data-stu-id="cac77-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="cac77-113">Cihaz bağlantı dizesi, IOT hub'ınıza bağlanmak için sanal cihazınız tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cac77-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="cac77-114">IOT hub bağlantı dizesine, IOT hub'ınıza bağlanmasına izin verilen cihazları yönetmek için IOT hub kimlik kayıt defterinde bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cac77-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="cac77-115">Kaynak grubunuzdaki tüm IOT hub aşağıdaki komutu çalıştırarak listesi:</span><span class="sxs-lookup"><span data-stu-id="cac77-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="cac77-116">Kullanım `iot-gateway` değeri olarak `{resource group name}` onu değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="cac77-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="cac77-117">IOT hub bağlantı dizesine, aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="cac77-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="cac77-118">`{my hub name}`Ders 2'de belirtilen adıdır.</span><span class="sxs-lookup"><span data-stu-id="cac77-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="cac77-119">Örnek kod için cihaz bağlantısı</span><span class="sxs-lookup"><span data-stu-id="cac77-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="cac77-120">IOT hub ve cihaz bağlantısı yapılandırmalarını güncelleştirme `config-azure.json` aşağıdaki adımları gerçekleştirerek:</span><span class="sxs-lookup"><span data-stu-id="cac77-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="cac77-121">Açık `config-azure.json` Visual Studio konsol penceresinde aşağıdaki komutu çalıştırarak kod:</span><span class="sxs-lookup"><span data-stu-id="cac77-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="cac77-122">İçinde aşağıdaki değişiklikleri yapın `config-azure.json` dosyası:</span><span class="sxs-lookup"><span data-stu-id="cac77-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![azure yapılandırma ekran görüntüsü](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="cac77-124">Değiştir `[IoT hub connection string]` IOT hub bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="cac77-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="cac77-125">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="cac77-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="cac77-126">Sanal cihaz örnek uygulamayı çalıştırın ve IOT Hub aşağıdaki komutla iletilerini okuyun:</span><span class="sxs-lookup"><span data-stu-id="cac77-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="cac77-127">Komut iletileri 2 saniyede IOT hub'ınıza gönderir uygulama çalışır.</span><span class="sxs-lookup"><span data-stu-id="cac77-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="cac77-128">İleti almak için bir alt işlem olarak çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="cac77-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="cac77-129">Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cac77-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="cac77-130">Uygulama 40 saniye cinsinden çıkılacak.</span><span class="sxs-lookup"><span data-stu-id="cac77-130">The application will exit in 40 seconds.</span></span>

![Gönderilen ve alınan ileti ile sanal örnek uygulama](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="cac77-132">Özet</span><span class="sxs-lookup"><span data-stu-id="cac77-132">Summary</span></span>

<span data-ttu-id="cac77-133">İle sanal cihaz IOT hub'ınıza veri göndermek için örnek uygulama başarıyla çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="cac77-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="cac77-134">Ayrıca, IOT hub'a gönderilen iletileri okuduğunuz.</span><span class="sxs-lookup"><span data-stu-id="cac77-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cac77-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cac77-135">Next steps</span></span>
[<span data-ttu-id="cac77-136">Azure işlev uygulaması ve Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cac77-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


