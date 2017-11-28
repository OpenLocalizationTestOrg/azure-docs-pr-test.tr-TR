---
title: "aaaSimulated Raspberry Pi'yi toocloud (Node.js) - bağlanmak Raspberry Pi'yi web simulator tooAzure IOT hub'ı | Microsoft Docs"
description: "Raspberry Pi'yi toosend veri toohello Azure bulut için Raspberry Pi'yi web simulator tooAzure IOT hub'ı bağlayın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Böğürtlenli pi simulator, azure IOT Böğürtlenli pi Böğürtlenli PI IOT hub, Böğürtlenli pi veri toocloud, Böğürtlenli PI toocloud Gönder"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="42e74-104">Raspberry Pi'yi çevrimiçi simulator tooAzure IOT hub'ı (Node.js) bağlanma</span><span class="sxs-lookup"><span data-stu-id="42e74-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="42e74-105">Bu öğreticide, Raspberry Pi'yi çevrimiçi simulator ile çalışmanın hello temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="42e74-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="42e74-106">Daha sonra nasıl tooseamlessly bağlanacağını hello Pi simulator toohello bulut kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="42e74-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="42e74-107">Fiziksel cihazlarınız varsa, ziyaret [bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı](iot-hub-raspberry-pi-kit-node-get-started.md) tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="42e74-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="42e74-108">Neler</span><span class="sxs-lookup"><span data-stu-id="42e74-108">What you do</span></span>

* <span data-ttu-id="42e74-109">Raspberry Pi'yi çevrimiçi simulator Hello temellerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="42e74-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="42e74-110">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42e74-110">Create an IoT hub.</span></span>
* <span data-ttu-id="42e74-111">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="42e74-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="42e74-112">Örnek bir uygulama Pi benzetimli toosend algılayıcı verileri tooyour IOT hub'ına çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="42e74-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="42e74-113">Oluşturduğunuz sanal Raspberry Pi'yi tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="42e74-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="42e74-114">Sonra hello simulator toogenerate algılayıcı verileri ile bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="42e74-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="42e74-115">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="42e74-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="42e74-116">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="42e74-116">What you learn</span></span>

* <span data-ttu-id="42e74-117">Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="42e74-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="42e74-118">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="42e74-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="42e74-119">Nasıl toowork Raspberry Pi'yi çevrimiçi simulator ile.</span><span class="sxs-lookup"><span data-stu-id="42e74-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="42e74-120">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="42e74-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="42e74-121">Raspberry Pi'yi web simulator genel bakış</span><span class="sxs-lookup"><span data-stu-id="42e74-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="42e74-122">Merhaba düğmesi toolaunch Raspberry Pi'yi çevrimiçi simülatörü'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="42e74-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="42e74-123">Raspberry Pi'yi simulator Başlat</span><span class="sxs-lookup"><span data-stu-id="42e74-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="42e74-124">Merhaba web benzeticisinde üç alan vardır.</span><span class="sxs-lookup"><span data-stu-id="42e74-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="42e74-125">Derleme - hello varsayılan hattı bir Pi BME280 algılayıcı ve bir LED bağlayan alanıdır.</span><span class="sxs-lookup"><span data-stu-id="42e74-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="42e74-126">Merhaba alanı Önizleme sürümünde kilitli özelleştirme bu nedenle şu anda yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="42e74-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="42e74-127">Alanı - toocode ile Raspberry Pi'yi için bir çevrimiçi kod düzenleyicisini kodlama.</span><span class="sxs-lookup"><span data-stu-id="42e74-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="42e74-128">Merhaba varsayılan örnek uygulaması toocollect algılayıcı verilerini BME280 algılayıcı yardımcı olur ve tooyour Azure IOT Hub gönderir.</span><span class="sxs-lookup"><span data-stu-id="42e74-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="42e74-129">Merhaba uygulaması ile gerçek Pi cihazları tamamen uyumludur.</span><span class="sxs-lookup"><span data-stu-id="42e74-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="42e74-130">Tümleşik konsol penceresi - kodunuzu hello çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="42e74-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="42e74-131">Bu pencere Hello üstünde üç düğme bulunur.</span><span class="sxs-lookup"><span data-stu-id="42e74-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="42e74-132">**Çalıştırma** -alan kodlama hello hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="42e74-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="42e74-133">**Sıfırlama** -sıfırlama hello alanı toohello varsayılan örnek uygulaması kodlama.</span><span class="sxs-lookup"><span data-stu-id="42e74-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="42e74-134">**Katlama/genişletme** - hello sağ tarafı var olan bir düğme, toofold ve genişletin konsol penceresinde hello için açık.</span><span class="sxs-lookup"><span data-stu-id="42e74-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="42e74-135">Merhaba Raspberry Pi'yi web simulator Önizleme sürümünde kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="42e74-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="42e74-136">Toohear isteriz sesinizi hello içinde [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="42e74-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="42e74-137">Merhaba kaynak kodu üzerinde ortak [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="42e74-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Pi çevrimiçi simulator genel bakış](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="42e74-139">Örnek bir uygulama Pi web simulator'da çalıştırma</span><span class="sxs-lookup"><span data-stu-id="42e74-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="42e74-140">Alan kodlama Merhaba varsayılan örnek uygulaması üzerinde çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="42e74-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="42e74-141">Satır 15 Hello yer tutucu hello Azure IOT hub cihaz bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="42e74-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="42e74-142">![Merhaba cihaz bağlantı dizesini değiştirin](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="42e74-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="42e74-143">Tıklatın **çalıştırmak** veya türü `npm start` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="42e74-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="42e74-144">Aşağıdaki hello çıktı hello algılayıcı verilerini ve tooyour IOT hub gönderilen Merhaba iletileri gösterir görmelisiniz ![çıktısı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="42e74-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="42e74-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42e74-145">Next steps</span></span>

<span data-ttu-id="42e74-146">Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42e74-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
