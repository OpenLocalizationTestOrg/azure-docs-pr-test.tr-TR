---
title: "Sanal cihaz & Azure IOT ağ geçidi - Başlarken | Microsoft Docs"
description: "IOT ağ geçidi Starter Kit ile çalışmaya başlama, Azure IOT hub'ınızı oluşturun ve IOT hub'ı ağ geçidine bağlanmak"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub, IOT ağ geçidi, noktalar, IOT Araç Seti Internet ile çalışmaya başlama"
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
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="9e3c7-104">IOT ağ geçidi Starter Kit ile bir sanal cihaz ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9e3c7-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e3c7-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="9e3c7-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="9e3c7-106">Sanal cihaz</span><span class="sxs-lookup"><span data-stu-id="9e3c7-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="9e3c7-107">Bu öğreticide, ile çalışmanın temelleri öğrenerek başlamadan [IOT ağ geçidi Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="9e3c7-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="9e3c7-108">Intel NUC ile Rüzgar Akarsu Linux çalıştıran çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="9e3c7-109">Şunları öğreneceksiniz seamleesly için Azure IOT hub'ı kullanarak bulut aygıtlarınıza nasıl bağlanacağını.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="9e3c7-110">**Bir pakete henüz yok mu?:** tıklatın [burada](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="9e3c7-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="9e3c7-111">Ders 1: NUC cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e3c7-111">Lesson 1: Configure your NUC</span></span>
![Lesson1 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="9e3c7-113">Bu ders, Intel NUC (sonraki birim, bilgisayar) bir Azure IOT ağ geçidi olarak Seti'nde ayarlama, Azure IOT kenar paket üzerinde NUC yükleyin ve bir örnek uygulama ağ geçidi işlevlerini doğrulayın çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="9e3c7-114">*Tahmini tamamlanma süresi: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="9e3c7-115">Git [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="9e3c7-116">Ders 2: IoT Hub'ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e3c7-116">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="9e3c7-118">Bu ders, ana bilgisayara yazılım ve araçları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="9e3c7-119">Ardından, ücretsiz Azure hesabınızı oluşturmak, Azure IOT hub'ınızı sağlamak ve ilk Cihazınızı IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="9e3c7-120">Bu ders başlamadan önce Ders 1 tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="9e3c7-121">Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="9e3c7-121">Get the tools</span></span>
<span data-ttu-id="9e3c7-122">Yazılım ve araçları, ana bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="9e3c7-123">*Tahmini tamamlanma süresi: 20 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="9e3c7-124">Git [araçları edinin](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="9e3c7-125">IOT hub'ı oluşturma ve Cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="9e3c7-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="9e3c7-126">Kaynak grubu oluşturmak, ilk Azure IOT hub'ınızı sağlamak ve Azure CLI kullanarak IOT hub'ına ilk aygıtınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="9e3c7-127">*Tahmini tamamlanma süresi: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="9e3c7-128">Git [IOT hub'ı oluşturma ve Cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="9e3c7-129">Ders 3: sanal cihaz iletileri almak ve IOT hub'ından iletileri okur</span><span class="sxs-lookup"><span data-stu-id="9e3c7-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="9e3c7-130">Bu ders, yapılandırma ve sanal cihaz uygulaması yürütülmesini, ağ geçidi otomatikleştirmek için komut dosyalarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="9e3c7-131">Sanal cihaz uygulamasının örnek sıcaklık verileri oluşturur ve bir IOT hub modülüne gönderir.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="9e3c7-132">IOT hub modülü alınan verileri paketler ve Azure IOT Edge'de sağlanan ağ geçidi çerçevesi aracılığıyla IOT hub'ınıza gönderir.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Ders 3 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="9e3c7-134">Yapılandırma ve bir sanal cihaz çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9e3c7-134">Configure and run a simulated device</span></span>
<span data-ttu-id="9e3c7-135">Örnek kodları hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-135">Prepare the sample codes.</span></span> <span data-ttu-id="9e3c7-136">Ardından yapılandırın ve sanal cihaz örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="9e3c7-137">*Tahmini tamamlanma süresi: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="9e3c7-138">Git [yapılandırma ve çalıştırma bir sanal cihaz](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9e3c7-139">IOT hub'ından iletilerini okuyun</span><span class="sxs-lookup"><span data-stu-id="9e3c7-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="9e3c7-140">Örnek kod, IOT hub'ından iletileri okumak için ana bilgisayarınız çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="9e3c7-141">*Tahmini tamamlanma süresi: 15 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="9e3c7-142">Git [IOT hub'ından iletilerini okuyun](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="9e3c7-143">Ders 4: İletileri Azure Tablo depolamaya kaydetme</span><span class="sxs-lookup"><span data-stu-id="9e3c7-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="9e3c7-144">IOT hub'ından gelen iletileri alır ve bunları Azure Table depolama alanına yazan bir Azure işlevi uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Ders 4 uçtan uca diyagramı](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="9e3c7-146">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="9e3c7-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="9e3c7-147">Bir Azure işlevi uygulama ve bir Azure Storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="9e3c7-148">*Tahmini tamamlanma süresi: 10 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="9e3c7-149">Git [bir Azure işlevi uygulama ve Azure depolama hesabı oluştur](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="9e3c7-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="9e3c7-150">İletileri okuma Azure tablo Depolama'da kalıcı</span><span class="sxs-lookup"><span data-stu-id="9e3c7-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="9e3c7-151">Azure Table depolama alanına yazılır gibi ağ geçidi bulut iletileri izleyin.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="9e3c7-152">*Tahmini tamamlanma süresi: 5 dakika*</span><span class="sxs-lookup"><span data-stu-id="9e3c7-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="9e3c7-153">Git [iletilerini okuma Azure Table storage ' kalıcı](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9e3c7-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9e3c7-154">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9e3c7-154">Troubleshooting</span></span>
<span data-ttu-id="9e3c7-155">Çözümlerinde dersleri sırasında herhangi bir sorun varsa, arayın [sorun giderme](iot-hub-gateway-kit-c-sim-troubleshooting.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="9e3c7-156">Daha fazlasını keşfedin</span><span class="sxs-lookup"><span data-stu-id="9e3c7-156">Explore more</span></span>
<span data-ttu-id="9e3c7-157">Ziyaret [Intel IOT ağ geçidi Seti Geliştirici bölge](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9e3c7-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>