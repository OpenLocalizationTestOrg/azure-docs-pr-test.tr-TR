---
title: 'Azure IOT - Ders 3 Connect Arduino (C): Tablo depolama | Microsoft Docs'
description: "Azure Table depolama alanına yazılır gibi cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="dd605-104">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="dd605-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="dd605-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="dd605-105">What you will do</span></span>
<span data-ttu-id="dd605-106">İletileri Azure Table depolama alanına yazılır gibi Adafruit yumuşatma M0 WiFi Arduino panonuzu IOT hub'ına gönderilen cihaz bulut iletilerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd605-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span></span>

<span data-ttu-id="dd605-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="dd605-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dd605-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="dd605-108">What you will learn</span></span>
<span data-ttu-id="dd605-109">Bu makalede, gulp okuma ileti görevi iletileri, Azure tablo Depolama'da kalıcı okumak için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="dd605-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dd605-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="dd605-110">What you need</span></span>
<span data-ttu-id="dd605-111">Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Arduino Panonuzda Azure blink örnek uygulamayı çalıştırın][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="dd605-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="dd605-112">Depolama hesabınızdan yeni iletiler okuma</span><span class="sxs-lookup"><span data-stu-id="dd605-112">Read new messages from your storage account</span></span>
<span data-ttu-id="dd605-113">Önceki makalede örnek uygulama Arduino Panonuzda verdi.</span><span class="sxs-lookup"><span data-stu-id="dd605-113">In the previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="dd605-114">Azure IOT hub'ınıza örnek uygulama gönderilen iletileri.</span><span class="sxs-lookup"><span data-stu-id="dd605-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="dd605-115">IOT hub'ına gönderilen iletileri Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="dd605-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="dd605-116">Azure Table depolama hesabınızdan iletileri okumak için Azure depolama bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd605-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="dd605-117">Azure Table storage'da depolanan iletileri okumak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dd605-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="dd605-118">Bağlantı dizesi, aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="dd605-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="dd605-119">İlk komut alır `storage name` , ikinci komutta bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd605-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="dd605-120">Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="dd605-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="dd605-121">Yapılandırma dosyasını açın `config-arduino.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="dd605-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="dd605-122">Değiştir `[Azure storage connection string]` 1. adımda aldığınız bağlantı dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="dd605-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="dd605-123">Kaydet `config-arduino.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="dd605-123">Save the `config-arduino.json` file.</span></span>
5. <span data-ttu-id="dd605-124">İletileri yeniden göndermek ve bunları aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:</span><span class="sxs-lookup"><span data-stu-id="dd605-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="dd605-125">Azure Table depolama veri okuma mantığını bulunduğu `azure-table.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="dd605-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![çalıştırma--gulp okuma depolama][gulp-run]

## <a name="summary"></a><span data-ttu-id="dd605-127">Özet</span><span class="sxs-lookup"><span data-stu-id="dd605-127">Summary</span></span>
<span data-ttu-id="dd605-128">Başarılı bir şekilde bulutta IOT hub'ınıza Arduino panonuzu bağlı ve cihaz bulut iletilerini göndermek için kullanılan blink örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="dd605-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="dd605-129">Azure işlev uygulaması, Azure Table depolama alanına gelen IOT hub iletileri depolamak için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd605-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="dd605-130">Şimdi, IOT hub'ından Arduino panonuzu bulut cihaz iletileri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="dd605-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd605-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd605-131">Next steps</span></span>
<span data-ttu-id="dd605-132">[Bulut cihaza ileti gönderme][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="dd605-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md