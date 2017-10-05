---
title: "Azure IOT - Ders 3 Intel Edison'u (düğüm) bağlanma: işlev uygulaması oluşturma | Microsoft Docs"
description: "Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6ada1cbbb560f1373346eca561dceb28d7ca7242
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="3b9ac-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="3b9ac-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="3b9ac-105">[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) bulutta.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="3b9ac-106">Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="3b9ac-107">Ne</span><span class="sxs-lookup"><span data-stu-id="3b9ac-107">What will you do</span></span>
<span data-ttu-id="3b9ac-108">Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="3b9ac-109">Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="3b9ac-110">Depolama hesabı kalıcı iletilerin kopyalarını Azure tablosundan okumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="3b9ac-111">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="3b9ac-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="3b9ac-112">Ne size bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="3b9ac-112">What will you learn</span></span>
<span data-ttu-id="3b9ac-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3b9ac-113">In this article, you will learn:</span></span>
* <span data-ttu-id="3b9ac-114">Nasıl kullanılacağını [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="3b9ac-115">IOT hub iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="3b9ac-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="3b9ac-116">Ne ihtiyacınız var</span><span class="sxs-lookup"><span data-stu-id="3b9ac-116">What do you need</span></span>
<span data-ttu-id="3b9ac-117">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b9ac-117">You must have successfully completed:</span></span>
- <span data-ttu-id="3b9ac-118">[Intel Edison'u ile çalışmaya başlama][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="3b9ac-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="3b9ac-119">[Azure IOT hub'ınızı oluşturma][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="3b9ac-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="3b9ac-120">Örnek uygulamayı açın</span><span class="sxs-lookup"><span data-stu-id="3b9ac-120">Open the sample app</span></span>
<span data-ttu-id="3b9ac-121">Örnek Proje aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="3b9ac-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* <span data-ttu-id="3b9ac-123">Dosyada `app` alt anahtarı kaynağı dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="3b9ac-124">Bu kaynak dosyası 20 kez IOT hub'ınıza ileti gönderme ve LED, gönderdiği her ileti için blink kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="3b9ac-125">`arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="3b9ac-126">`arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="3b9ac-127">`ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="3b9ac-128">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b9ac-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="3b9ac-129">Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri][arm-template-parameters]

* <span data-ttu-id="3b9ac-131">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Intel Edison'u kayıtlı][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="3b9ac-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="3b9ac-132">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="3b9ac-133">Önek, kaynak adı çakışmayı önlemek için genel benzersiz olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="3b9ac-134">Bir çizgi ya da rakamla önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="3b9ac-135">Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:</span><span class="sxs-lookup"><span data-stu-id="3b9ac-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="3b9ac-136">Bu kaynakları oluşturmak için yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="3b9ac-137">Kaynak oluşturma işlemi devam ederken, sonraki makalede hareket ettirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="3b9ac-138">Özet</span><span class="sxs-lookup"><span data-stu-id="3b9ac-138">Summary</span></span>
<span data-ttu-id="3b9ac-139">IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="3b9ac-140">Şimdi, dağıtın ve üzerinde Edison'u cihaz bulut iletilerini göndermek için örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3b9ac-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b9ac-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b9ac-141">Next steps</span></span>
<span data-ttu-id="3b9ac-142">[Intel Edison'u üzerinde cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="3b9ac-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md