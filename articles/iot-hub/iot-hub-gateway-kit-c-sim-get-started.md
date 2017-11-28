---
title: "Sanal cihaz & Azure IOT ağ geçidi - Başlarken | Microsoft Docs"
description: "IOT ağ geçidi Starter Kit ile çalışmaya başlama, Azure IOT hub'ınızı oluşturun ve ağ geçidi toohello IOT hub'ı Bağlan"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub, IOT ağ geçidi, Başlarken hello nesnelerin interneti, IOT Araç Seti"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="10d0e-104">IOT ağ geçidi Starter Kit ile bir sanal cihaz ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="10d0e-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="10d0e-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="10d0e-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="10d0e-106">Sanal cihaz</span><span class="sxs-lookup"><span data-stu-id="10d0e-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="10d0e-107">Bu öğreticide, ile çalışmanın temelleri hello öğrenerek başlamadan [IOT ağ geçidi Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="10d0e-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="10d0e-108">Intel NUC ile Rüzgar Akarsu Linux çalıştıran çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="10d0e-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="10d0e-109">Nasıl tooseamleesly bağlanacağını aygıtları toohello bulut Azure IOT hub'ı kullanarak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="10d0e-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="10d0e-110">**Bir pakete henüz yok mu?:** tıklatın [burada](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="10d0e-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="10d0e-111">Ders 1: NUC cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10d0e-111">Lesson 1: Configure your NUC</span></span>
![Lesson1 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="10d0e-113">Bu ders içinde Intel NUC (sonraki birim, bilgisayar) hello Seti Azure IOT ağ geçidi olarak ayarlamak, NUC üzerinde hello Azure IOT kenar paketi yükleyin ve bir örnek uygulama tooverify hello ağ geçidi işlevi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="10d0e-114">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="10d0e-115">Çok Git[Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="10d0e-116">Ders 2: IoT Hub'ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="10d0e-116">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="10d0e-118">Bu alıştırmanın ilerisinde ana bilgisayarınızda hello araçları ve yazılımını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="10d0e-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="10d0e-119">Ardından, ücretsiz Azure hesabı oluşturun, Azure IOT hub'ınızı sağlamanıza ve ilk aygıtınızı hello IOT hub'ı oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="10d0e-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="10d0e-120">Bu ders başlamadan önce Ders 1 tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="10d0e-121">Merhaba araçları edinin</span><span class="sxs-lookup"><span data-stu-id="10d0e-121">Get hello tools</span></span>
<span data-ttu-id="10d0e-122">Merhaba araçları ve yazılım, ana bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="10d0e-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="10d0e-123">*Zaman toocomplete tahmini: 20 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="10d0e-124">Çok Git[alma hello araçları](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="10d0e-125">IOT hub'ı oluşturma ve Cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="10d0e-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="10d0e-126">Kaynak grubu oluşturmak, ilk Azure IOT hub'ınızı sağlamak ve hello Azure CLI kullanarak ilk aygıt toohello IOT hub'ınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="10d0e-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="10d0e-127">*Zaman toocomplete tahmini: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="10d0e-128">Çok Git[IOT hub'ı oluşturma ve Cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="10d0e-129">Ders 3: hello benzetimli aygıttan iletileri almasına ve IOT hub'ından iletileri okur</span><span class="sxs-lookup"><span data-stu-id="10d0e-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="10d0e-130">Bu alıştırmanın ilerisinde, ağ geçidi betikleri tooautomate hello yapılandırması ve sanal cihaz uygulaması yürütülmesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="10d0e-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="10d0e-131">Merhaba sanal cihaz uygulamasının örnek sıcaklık verileri oluşturur ve tooan IOT hub modül gönderir.</span><span class="sxs-lookup"><span data-stu-id="10d0e-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="10d0e-132">IOT hub modülü paketleri Hello veri tooyour IOT hub'ı sağlanan hello ağ geçidi çerçevesi aracılığıyla Azure IOT Edge'de gönderir ve alınan hello.</span><span class="sxs-lookup"><span data-stu-id="10d0e-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Ders 3 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="10d0e-134">Yapılandırma ve bir sanal cihaz çalıştırma</span><span class="sxs-lookup"><span data-stu-id="10d0e-134">Configure and run a simulated device</span></span>
<span data-ttu-id="10d0e-135">Merhaba örnek kodları hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-135">Prepare hello sample codes.</span></span> <span data-ttu-id="10d0e-136">Ardından yapılandırıp benzetimli hello aygıt örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="10d0e-137">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="10d0e-138">Çok Git[yapılandırma ve çalıştırma bir sanal cihaz](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="10d0e-139">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="10d0e-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="10d0e-140">Örnek kod, IOT hub'ından ana bilgisayar tooread hello iletilerde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="10d0e-141">*Zaman toocomplete tahmini: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="10d0e-142">Çok Git[IOT hub'ından iletilerini okuyun](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="10d0e-143">Ders 4: iletileri tooAzure tablo depolama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="10d0e-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="10d0e-144">IOT hub'ından gelen iletileri alır ve bunları tooAzure Table storage yazan bir Azure işlevi uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="10d0e-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Ders 4 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="10d0e-146">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="10d0e-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="10d0e-147">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure Storage hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="10d0e-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="10d0e-148">*Zaman toocomplete tahmini: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="10d0e-149">Çok Git[bir Azure işlevi uygulama ve Azure depolama hesabı oluştur](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="10d0e-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="10d0e-150">İletileri okuma Azure tablo Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="10d0e-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="10d0e-151">TooAzure Table storage yazıldığı şekilde hello ağ geçidi bulut iletileri izleyin.</span><span class="sxs-lookup"><span data-stu-id="10d0e-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="10d0e-152">*Zaman toocomplete tahmini: 5 dakika*</span><span class="sxs-lookup"><span data-stu-id="10d0e-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="10d0e-153">Çok Git[iletilerini okuma Azure Table storage ' kalıcı](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="10d0e-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="10d0e-154">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="10d0e-154">Troubleshooting</span></span>
<span data-ttu-id="10d0e-155">Merhaba çözümlerinde hello dersleri sırasında herhangi bir sorun varsa, arayın [sorun giderme](iot-hub-gateway-kit-c-sim-troubleshooting.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="10d0e-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="10d0e-156">Daha fazlasını keşfedin</span><span class="sxs-lookup"><span data-stu-id="10d0e-156">Explore more</span></span>
<span data-ttu-id="10d0e-157">Merhaba ziyaret [Intel IOT ağ geçidi Seti Geliştirici bölge](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="10d0e-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
