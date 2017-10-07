---
featureFlags: usabilla
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: Tablo depolama | Microsoft Docs"
description: "Azure Table storage'ı tooyour yazıldığı şekilde hello cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="de42a-104">İletileri okuma Azure Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="de42a-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="de42a-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="de42a-105">What you will do</span></span>
<span data-ttu-id="de42a-106">Merhaba iletileri olarak Raspberry Pi 3 tooyour IOT hub'ından gönderilen İzleyicisi Merhaba cihaz bulut iletilerini tooyour Azure Table depolama yazılır.</span><span class="sxs-lookup"><span data-stu-id="de42a-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="de42a-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="de42a-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="de42a-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="de42a-108">What you will learn</span></span>
<span data-ttu-id="de42a-109">Bu makalede, Azure Table storage ' nasıl toouse Merhaba gulp okuma ileti görevi tooread iletileri kalıcı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="de42a-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="de42a-110">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="de42a-110">What you need</span></span>
<span data-ttu-id="de42a-111">Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Raspberry Pi 3'te hello Azure blink örnek uygulamayı çalıştırın](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="de42a-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="de42a-112">Depolama hesabınızdan yeni iletiler okuma</span><span class="sxs-lookup"><span data-stu-id="de42a-112">Read new messages from your storage account</span></span>
<span data-ttu-id="de42a-113">Merhaba önceki makalede örnek bir uygulama üzerinde Pi verdi.</span><span class="sxs-lookup"><span data-stu-id="de42a-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="de42a-114">Merhaba örnek uygulaması tooyour Azure IOT hub'ı iletileri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="de42a-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="de42a-115">tooyour IOT hub'a gönderilen Merhaba iletileri hello Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="de42a-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="de42a-116">Azure Table storage'hello Azure depolama bağlantı dizesi tooread iletileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="de42a-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="de42a-117">Azure Table depolama biriminde, depolanan tooread iletiler şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="de42a-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="de42a-118">Hello bağlantı dizesi hello aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="de42a-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="de42a-119">Merhaba ilk komut alır hello `storage name` hello ikinci komutu tooget hello bağlantı dizesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de42a-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="de42a-120">Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.</span><span class="sxs-lookup"><span data-stu-id="de42a-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="de42a-121">Açık hello yapılandırma dosyası `config-raspberrypi.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="de42a-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="de42a-122">Değiştir `[Azure storage connection string]` 1. adımda aldığınız hello bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="de42a-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="de42a-123">Merhaba Kaydet `config-raspberrypi.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="de42a-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="de42a-124">İletileri yeniden göndermek ve bunları hello aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:</span><span class="sxs-lookup"><span data-stu-id="de42a-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="de42a-125">Hello Azure Table depolama veri okuma için mantığı olan hello `azure-table.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="de42a-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
    ![çalıştırma--gulp okuma depolama](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="de42a-127">Özet</span><span class="sxs-lookup"><span data-stu-id="de42a-127">Summary</span></span>
<span data-ttu-id="de42a-128">Başarıyla Pi tooyour IOT hub'hello bulutta bağlı ve hello blink örnek uygulama toosend cihaz bulut iletilerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de42a-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="de42a-129">Ayrıca, hello Azure işlevi uygulama toostore gelen IOT hub iletileri tooyour Azure Table depolama de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de42a-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="de42a-130">Şimdi, IOT hub tooPi bulut-cihaz iletilerini gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de42a-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de42a-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de42a-131">Next steps</span></span>
[<span data-ttu-id="de42a-132">Merhaba örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="de42a-132">Run hello sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

