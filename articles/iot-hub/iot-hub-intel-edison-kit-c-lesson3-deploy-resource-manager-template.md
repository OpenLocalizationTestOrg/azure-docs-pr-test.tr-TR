---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 3: işlev uygulaması oluşturma | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="60716-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="60716-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="60716-105">[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="60716-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="60716-106">Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="60716-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="60716-107">Ne</span><span class="sxs-lookup"><span data-stu-id="60716-107">What will you do</span></span>
<span data-ttu-id="60716-108">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="60716-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="60716-109">Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.</span><span class="sxs-lookup"><span data-stu-id="60716-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="60716-110">Merhaba depolama hesabı okumak için kullanılan hello Azure tablosundan iletilerin kopyalarını kalıcı.</span><span class="sxs-lookup"><span data-stu-id="60716-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="60716-111">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="60716-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="60716-112">Ne size bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="60716-112">What will you learn</span></span>
<span data-ttu-id="60716-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="60716-113">In this article, you will learn:</span></span>
* <span data-ttu-id="60716-114">Nasıl toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="60716-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="60716-115">Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.</span><span class="sxs-lookup"><span data-stu-id="60716-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="60716-116">Ne ihtiyacınız var</span><span class="sxs-lookup"><span data-stu-id="60716-116">What do you need</span></span>
<span data-ttu-id="60716-117">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="60716-117">You must have successfully completed:</span></span>
- <span data-ttu-id="60716-118">[Intel Edison'u ile çalışmaya başlama][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="60716-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="60716-119">[Azure IOT hub'ınızı oluşturma][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="60716-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="60716-120">Açık hello örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="60716-120">Open hello sample app</span></span>
<span data-ttu-id="60716-121">Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="60716-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* <span data-ttu-id="60716-123">Merhaba Hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="60716-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="60716-124">Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.</span><span class="sxs-lookup"><span data-stu-id="60716-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="60716-125">Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="60716-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="60716-126">Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="60716-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="60716-127">Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="60716-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="60716-128">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="60716-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="60716-129">Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="60716-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri][arm-template-parameters]

* <span data-ttu-id="60716-131">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Intel Edison'u kayıtlı][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="60716-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="60716-132">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="60716-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="60716-133">Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar.</span><span class="sxs-lookup"><span data-stu-id="60716-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="60716-134">Bir çizgi ya da rakamla hello önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="60716-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="60716-135">Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:</span><span class="sxs-lookup"><span data-stu-id="60716-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="60716-136">Bu kaynakları toocreate yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="60716-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="60716-137">Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60716-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="60716-138">Özet</span><span class="sxs-lookup"><span data-stu-id="60716-138">Summary</span></span>
<span data-ttu-id="60716-139">IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler.</span><span class="sxs-lookup"><span data-stu-id="60716-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="60716-140">Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Edison'u üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="60716-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60716-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60716-141">Next steps</span></span>
<span data-ttu-id="60716-142">[Örnek uygulama toosend cihaz bulut iletilerini Intel Edison'u üzerinde çalıştırmak][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="60716-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md