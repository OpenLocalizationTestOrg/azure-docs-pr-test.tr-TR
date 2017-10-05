---
title: 'Azure IOT - Ders 3 Connect Intel Edison (C): izleme iletileri | Microsoft Docs'
description: "Azure Table depolama alanına yazılır gibi cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 249b5e0e96051fa2adeedfb9befd98fc939b4d40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="c844b-104">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="c844b-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c844b-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="c844b-105">What you will do</span></span>
<span data-ttu-id="c844b-106">İletileri Azure Table depolama alanına yazılır gibi Intel Edison'u IOT hub'ına gönderilen cihaz bulut iletilerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="c844b-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="c844b-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c844b-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c844b-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="c844b-108">What you will learn</span></span>
<span data-ttu-id="c844b-109">Bu makalede, gulp okuma ileti görevi iletileri, Azure tablo Depolama'da kalıcı okumak için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c844b-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c844b-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c844b-110">What you need</span></span>
<span data-ttu-id="c844b-111">Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Intel Edison'u üzerinde Azure blink örnek uygulamayı çalıştırın][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="c844b-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="c844b-112">Depolama hesabınızdan yeni iletiler okuma</span><span class="sxs-lookup"><span data-stu-id="c844b-112">Read new messages from your storage account</span></span>
<span data-ttu-id="c844b-113">Önceki makalede örnek bir uygulama üzerinde Edison'u verdi.</span><span class="sxs-lookup"><span data-stu-id="c844b-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="c844b-114">Azure IOT hub'ınıza örnek uygulama gönderilen iletileri.</span><span class="sxs-lookup"><span data-stu-id="c844b-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="c844b-115">IOT hub'ına gönderilen iletileri Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="c844b-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="c844b-116">Azure Table depolama hesabınızdan iletileri okumak için Azure depolama bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c844b-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="c844b-117">Azure Table storage'da depolanan iletileri okumak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c844b-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="c844b-118">Bağlantı dizesi, aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="c844b-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="c844b-119">İlk komut alır `storage name` , ikinci komutta bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c844b-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="c844b-120">Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="c844b-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="c844b-121">Yapılandırma dosyasını açın `config-edison.json` aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c844b-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="c844b-122">Değiştir `[Azure storage connection string]` 1. adımda aldığınız bağlantı dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="c844b-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="c844b-123">Kaydet `config-edison.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="c844b-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="c844b-124">İletileri yeniden göndermek ve bunları aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:</span><span class="sxs-lookup"><span data-stu-id="c844b-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="c844b-125">Azure Table depolama veri okuma mantığını bulunduğu `azure-table.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="c844b-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![çalıştırma--gulp okuma depolama][gulp run]

## <a name="summary"></a><span data-ttu-id="c844b-127">Özet</span><span class="sxs-lookup"><span data-stu-id="c844b-127">Summary</span></span>
<span data-ttu-id="c844b-128">Başarılı bir şekilde bulutta IOT hub'ınıza Edison'u bağlı ve cihaz bulut iletilerini göndermek için kullanılan blink örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="c844b-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="c844b-129">Azure işlev uygulaması, Azure Table depolama alanına gelen IOT hub iletileri depolamak için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c844b-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="c844b-130">Şimdi, IOT hub'ından Edison'u için bulut cihaz iletileri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="c844b-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c844b-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c844b-131">Next steps</span></span>
<span data-ttu-id="c844b-132">[Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="c844b-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md