---
title: "Azure IOT - Ders 3 Raspberry Pi'yi (düğüm) bağlanma: şablon dağıtımı | Microsoft Docs"
description: "Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="adbd1-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="adbd1-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="adbd1-105">[Azure işlevleri](../azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) bulutta.</span><span class="sxs-lookup"><span data-stu-id="adbd1-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="adbd1-106">Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="adbd1-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="adbd1-107">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="adbd1-107">What you will do</span></span>
<span data-ttu-id="adbd1-108">Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="adbd1-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="adbd1-109">Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.</span><span class="sxs-lookup"><span data-stu-id="adbd1-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="adbd1-110">Herhangi bir sorun varsa, üzerinde çözümleri arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="adbd1-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="adbd1-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="adbd1-111">What you will learn</span></span>
<span data-ttu-id="adbd1-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="adbd1-112">In this article, you will learn:</span></span>

* <span data-ttu-id="adbd1-113">Nasıl kullanılacağını [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="adbd1-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="adbd1-114">IOT hub iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="adbd1-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="adbd1-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="adbd1-115">What you need</span></span>
<span data-ttu-id="adbd1-116">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="adbd1-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="adbd1-117">Raspberry Pi 3 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="adbd1-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="adbd1-118">Azure IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbd1-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="adbd1-119">Örnek uygulamayı açın</span><span class="sxs-lookup"><span data-stu-id="adbd1-119">Open the sample app</span></span>
<span data-ttu-id="adbd1-120">Örnek Proje aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="adbd1-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="adbd1-122">`app.js` Dosyasını `app` alt anahtarı kaynağı dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="adbd1-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="adbd1-123">Bu kaynak dosyası 20 kez IOT hub'ınıza ileti gönderme ve LED, gönderdiği her ileti için blink kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="adbd1-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="adbd1-124">`arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="adbd1-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="adbd1-125">`arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="adbd1-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="adbd1-126">`ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="adbd1-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="adbd1-127">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="adbd1-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="adbd1-128">Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="adbd1-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="adbd1-130">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Raspberry Pi 3 kayıtlı](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="adbd1-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="adbd1-131">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="adbd1-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="adbd1-132">Önek, kaynak adı çakışmayı önlemek için genel benzersiz olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="adbd1-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="adbd1-133">Bir çizgi ya da rakamla önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="adbd1-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="adbd1-134">Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:</span><span class="sxs-lookup"><span data-stu-id="adbd1-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="adbd1-135">Bu kaynakları oluşturmak için yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="adbd1-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="adbd1-136">Kaynak oluşturma işlemi devam ederken, sonraki makalede hareket ettirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adbd1-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="adbd1-137">Özet</span><span class="sxs-lookup"><span data-stu-id="adbd1-137">Summary</span></span>
<span data-ttu-id="adbd1-138">IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="adbd1-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="adbd1-139">Şimdi, dağıtın ve üzerinde Pi cihaz bulut iletilerini göndermek için örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="adbd1-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adbd1-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="adbd1-140">Next steps</span></span>
[<span data-ttu-id="adbd1-141">Raspberry Pi 3'te cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="adbd1-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

