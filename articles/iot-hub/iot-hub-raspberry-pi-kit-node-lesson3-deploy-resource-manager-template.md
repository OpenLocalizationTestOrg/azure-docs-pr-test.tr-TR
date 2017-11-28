---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: şablon dağıtımı | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
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
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2a9ca-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="2a9ca-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="2a9ca-105">[Azure işlevleri](../azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="2a9ca-106">Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2a9ca-107">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="2a9ca-107">What you will do</span></span>
<span data-ttu-id="2a9ca-108">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="2a9ca-109">Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="2a9ca-110">Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2a9ca-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2a9ca-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="2a9ca-111">What you will learn</span></span>
<span data-ttu-id="2a9ca-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2a9ca-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2a9ca-113">Nasıl toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-113">How toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="2a9ca-114">Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2a9ca-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="2a9ca-115">What you need</span></span>
<span data-ttu-id="2a9ca-116">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a9ca-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="2a9ca-117">Raspberry Pi 3 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2a9ca-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="2a9ca-118">Azure IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a9ca-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="2a9ca-119">Açık hello örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="2a9ca-119">Open hello sample app</span></span>
<span data-ttu-id="2a9ca-120">Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="2a9ca-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="2a9ca-122">Merhaba `app.js` hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-122">hello `app.js` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="2a9ca-123">Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="2a9ca-124">Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="2a9ca-125">Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="2a9ca-126">Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="2a9ca-127">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a9ca-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="2a9ca-128">Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="2a9ca-130">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Raspberry Pi 3 kayıtlı](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2a9ca-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="2a9ca-131">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="2a9ca-132">Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="2a9ca-133">Bir çizgi ya da rakamla hello önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="2a9ca-134">Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:</span><span class="sxs-lookup"><span data-stu-id="2a9ca-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="2a9ca-135">Bu kaynakları toocreate yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="2a9ca-136">Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="2a9ca-137">Özet</span><span class="sxs-lookup"><span data-stu-id="2a9ca-137">Summary</span></span>
<span data-ttu-id="2a9ca-138">IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="2a9ca-139">Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Pi üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a9ca-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a9ca-140">Next steps</span></span>
[<span data-ttu-id="2a9ca-141">Örnek uygulama toosend cihaz bulut iletilerini Raspberry Pi 3'te çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a9ca-141">Run a sample application toosend device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

