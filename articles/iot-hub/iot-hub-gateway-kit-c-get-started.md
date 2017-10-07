---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Başlarken | Microsoft Docs"
description: "IOT ağ geçidi Starter Kit ile çalışmaya başlama, Azure IOT hub'ınızı oluşturması ve SensorTag ve ağ geçidi toohello IOT hub Bağlan"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub, IOT ağ geçidi, Başlarken hello nesnelerin interneti, IOT Araç Seti"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="14fd8-104">IOT ağ geçidi Starter Kit bir SensorTag ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="14fd8-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="14fd8-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="14fd8-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="14fd8-106">Sanal cihaz</span><span class="sxs-lookup"><span data-stu-id="14fd8-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="14fd8-107">Bu öğreticide, ile çalışmanın temelleri hello öğrenerek başlamadan [IOT ağ geçidi Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="14fd8-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="14fd8-108">Intel NUC ile Rüzgar Akarsu Linux ve hello çalıştıran çalışma [tı SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="14fd8-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="14fd8-109">Nasıl tooseamleesly bağlanacağını aygıtları toohello bulut Azure IOT hub'ı kullanarak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="14fd8-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="14fd8-110">**Bir pakete henüz yok mu?:** tıklatın [burada](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="14fd8-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="14fd8-111">**Bir SensorTag yok mu?:** [Başlat ile bir sanal cihaz](iot-hub-gateway-kit-c-sim-get-started.md) veya [bir SensorTag satın alın](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="14fd8-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="14fd8-112">Ders 1: NUC cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="14fd8-112">Lesson 1: Configure your NUC</span></span>
![Lesson1 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="14fd8-114">Bu ders içinde Intel NUC (sonraki birim, bilgisayar) hello Seti Azure IOT ağ geçidi olarak ayarlamak, NUC üzerinde hello Azure IOT kenar paketi yükleyin ve bir örnek uygulama tooverify hello ağ geçidi işlevi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="14fd8-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="14fd8-115">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="14fd8-116">Çok Git[Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="14fd8-117">Ders 2: IoT Hub'ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="14fd8-117">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="14fd8-119">Bu alıştırmanın ilerisinde ana bilgisayarınızda hello araçları ve yazılımını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="14fd8-120">Ardından, ücretsiz Azure hesabı oluşturun, Azure IOT hub'ınızı sağlamanıza ve ilk aygıtınızı hello IOT hub'ı oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="14fd8-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="14fd8-121">Bu ders başlamadan önce Ders 1 tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="14fd8-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="14fd8-122">Merhaba araçları edinin</span><span class="sxs-lookup"><span data-stu-id="14fd8-122">Get hello tools</span></span>
<span data-ttu-id="14fd8-123">Merhaba araçları ve yazılım, ana bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="14fd8-124">*Zaman toocomplete tahmini: 20 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="14fd8-125">Çok Git[alma hello araçları](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="14fd8-126">IOT hub'ı oluşturma ve Cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="14fd8-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="14fd8-127">Kaynak grubu oluşturmak, ilk Azure IOT hub'ınızı sağlamak ve hello Azure CLI kullanarak ilk aygıt toohello IOT hub'ınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="14fd8-128">*Zaman toocomplete tahmini: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="14fd8-129">Çok Git[IOT hub'ı oluşturma ve Cihazınızı kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="14fd8-130">Ders 3: SensorTag iletileri almasına ve IOT hub'ından iletileri okur</span><span class="sxs-lookup"><span data-stu-id="14fd8-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="14fd8-131">Bu alıştırmanın ilerisinde, ağ geçidi betikleri tooautomate hello yapılandırma ve bırak örnek bir uygulama yürütülmesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="14fd8-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="14fd8-132">Bu tür uygulamalar modülleri tooaggregate ve dönüştürme veri koleksiyonu kullanmak, komutları işlemek veya herhangi bir sayıda ilişkili görevleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="14fd8-133">Modülleri başka bir işlemle bir ileti Aracısı iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="14fd8-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="14fd8-134">Merhaba örnek uygulaması bırak modülü ve bir IOT hub modülü vardır.</span><span class="sxs-lookup"><span data-stu-id="14fd8-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="14fd8-135">Merhaba bırak modülü bırak SensorTag verileri alır.</span><span class="sxs-lookup"><span data-stu-id="14fd8-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="14fd8-136">IOT hub modülü paketleri Hello veri tooyour IOT hub'ı sağlanan hello ağ geçidi çerçevesi aracılığıyla Azure IOT Edge'de gönderir ve alınan hello.</span><span class="sxs-lookup"><span data-stu-id="14fd8-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Ders 3 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="14fd8-138">Yapılandırma ve hello bırak örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="14fd8-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="14fd8-139">SensorTag ve ağ geçidiniz arasında hello bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="14fd8-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="14fd8-140">Ardından hello yapılandırmayı tamamlamak ve hello bırak örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="14fd8-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="14fd8-141">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="14fd8-142">Çok Git[yapılandırma ve çalıştırma hello bırak örnek uygulaması](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="14fd8-143">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="14fd8-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="14fd8-144">Örnek kod, IOT hub'ından bilgisayar tooread iletileri ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="14fd8-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="14fd8-145">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="14fd8-146">Çok Git[IOT hub'ından iletilerini okuyun](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="14fd8-147">Ders 4: iletileri tooAzure tablo depolama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="14fd8-148">IOT hub'ından gelen iletileri alır ve bunları tooAzure Table storage yazan bir Azure işlevi uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="14fd8-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Ders 4 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="14fd8-150">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="14fd8-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="14fd8-151">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure Storage hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="14fd8-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="14fd8-152">*Zaman toocomplete tahmini: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="14fd8-153">Çok Git[bir Azure işlevi uygulama ve Azure depolama hesabı oluştur](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="14fd8-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="14fd8-154">İletileri okuma Azure tablo Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="14fd8-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="14fd8-155">TooAzure Table storage yazıldığı şekilde hello ağ geçidi bulut iletileri izleyin.</span><span class="sxs-lookup"><span data-stu-id="14fd8-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="14fd8-156">*Zaman toocomplete tahmini: 5 dakika*</span><span class="sxs-lookup"><span data-stu-id="14fd8-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="14fd8-157">Çok Git[iletilerini okuma Azure Table storage ' kalıcı](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="14fd8-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="14fd8-158">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="14fd8-158">Troubleshooting</span></span>
<span data-ttu-id="14fd8-159">Merhaba çözümlerinde hello dersleri sırasında herhangi bir sorun varsa, arayın [sorun giderme](iot-hub-gateway-kit-c-troubleshooting.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="14fd8-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="14fd8-160">Daha fazlasını keşfedin</span><span class="sxs-lookup"><span data-stu-id="14fd8-160">Explore more</span></span>
<span data-ttu-id="14fd8-161">Merhaba ziyaret [Intel IOT ağ geçidi Seti Geliştirici bölge](http://software.intel.com/iot/microsoft-azure) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="14fd8-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
