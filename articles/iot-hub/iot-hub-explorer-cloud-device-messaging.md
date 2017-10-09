---
title: "iothub-Gezgini ile Mesajlaşma aaaManage Azure IOT Hub bulut cihaz | Microsoft Docs"
description: "Nasıl toouse iothub-explorer CLI aracı toomonitor aygıt toocloud (D2C) iletilerini hello bulut toodevice (C2D) iletileri ve Azure IOT hub'da gönderme öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "ıothub Gezgini, Mesajlaşma, bulut cihaz IOT hub bulut toodevice, bulut toodevice Mesajlaşma"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="612fc-104">Aygıt ve IOT hub'ı arasında ileti alıp ıothub explorer toosend kullanın</span><span class="sxs-lookup"><span data-stu-id="612fc-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="612fc-106">[ıothub explorer](https://github.com/azure/iothub-explorer) IOT hub'ı yönetimini kolaylaştırır komutları sayıda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="612fc-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="612fc-107">Bu öğretici odaklanılmaktadır toouse iothub-explorer toosend Cihazınızı ve IOT hub'ınız arasında ileti alıp.</span><span class="sxs-lookup"><span data-stu-id="612fc-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="612fc-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="612fc-108">What you will learn</span></span>

<span data-ttu-id="612fc-109">Hakkında bilgi edineceksiniz nasıl toouse iothub-explorer toomonitor cihaz bulut iletilerini ve toosend bulut-cihaz iletilerini.</span><span class="sxs-lookup"><span data-stu-id="612fc-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="612fc-110">Cihaz bulut iletilerini Cihazınızı toplar ve tooyour IOT hub'ı gönderir algılayıcı verilerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="612fc-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="612fc-111">Bulut-cihaz iletilerini IOT hub'ınızı bağlı tooyour aygıt bir LED tooyour aygıt tooblink gönderir komutları olabilir.</span><span class="sxs-lookup"><span data-stu-id="612fc-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="612fc-112">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="612fc-112">What you will do</span></span>

- <span data-ttu-id="612fc-113">Iothub explorer toomonitor cihaz bulut iletilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="612fc-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="612fc-114">Iothub explorer toosend bulut-cihaz iletilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="612fc-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="612fc-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="612fc-115">What you need</span></span>

- <span data-ttu-id="612fc-116">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="612fc-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="612fc-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="612fc-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="612fc-118">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="612fc-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="612fc-119">Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="612fc-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="612fc-120">iothub-Gezgini.</span><span class="sxs-lookup"><span data-stu-id="612fc-120">iothub-explorer.</span></span> <span data-ttu-id="612fc-121">([Yükleme ıothub explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="612fc-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="612fc-122">Cihaz bulut iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="612fc-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="612fc-123">cihaz tooyour IOT hub'dan gönderilen toomonitor iletileri şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="612fc-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="612fc-124">Bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="612fc-124">Open a console window.</span></span>
1. <span data-ttu-id="612fc-125">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="612fc-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="612fc-126">Alma `<device-id>` ve `<IoTHubConnectionString>` IOT hub'ınızı gelen.</span><span class="sxs-lookup"><span data-stu-id="612fc-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="612fc-127">Emin olun hello önceki öğreticiyi bitirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="612fc-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="612fc-128">Ya da toouse deneyebilirsiniz `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` varsa `HostName`, `SharedAccessKeyName` ve `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="612fc-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="612fc-129">Buluttan cihaza iletileri gönderme</span><span class="sxs-lookup"><span data-stu-id="612fc-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="612fc-130">toosend IOT hub tooyour cihazı iletiden şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="612fc-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="612fc-131">Bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="612fc-131">Open a console window.</span></span>
1. <span data-ttu-id="612fc-132">Bir oturum hello aşağıdaki komutu çalıştırarak, IOT hub'ına başlatın:</span><span class="sxs-lookup"><span data-stu-id="612fc-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="612fc-133">Bir ileti tooyour aygıt hello aşağıdaki komutu çalıştırarak gönder:</span><span class="sxs-lookup"><span data-stu-id="612fc-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="612fc-134">Merhaba komutu bağlı tooyour cihaz ve hello ileti tooyour cihaz gönderen hello ışığı yanıp.</span><span class="sxs-lookup"><span data-stu-id="612fc-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="612fc-135">Merhaba iletiyi aldıktan sonra ayrı ack komutu geri tooyour IOT hub hello aygıt toosend için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="612fc-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="612fc-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="612fc-136">Next steps</span></span>

<span data-ttu-id="612fc-137">Nasıl toomonitor cihaz-bulut iletileri ve bulut-cihaz iletilerini IOT cihaz ile Azure IOT hub'ı arasında göndermek öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="612fc-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
