---
title: "Connect Arduino (C) tooAzure IOT - Ders 3: şablon dağıtımı | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="1c757-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="1c757-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="1c757-105">[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="1c757-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="1c757-106">Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="1c757-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="1c757-107">Ne</span><span class="sxs-lookup"><span data-stu-id="1c757-107">What will you do</span></span>
<span data-ttu-id="1c757-108">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c757-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="1c757-109">Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.</span><span class="sxs-lookup"><span data-stu-id="1c757-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="1c757-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sayfa Adafruit yumuşatma M0 WiFi Arduino panonuz için sorun giderme](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1c757-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="1c757-111">Ne size bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="1c757-111">What will you learn</span></span>
<span data-ttu-id="1c757-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1c757-112">In this article, you will learn:</span></span>
* <span data-ttu-id="1c757-113">Nasıl toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1c757-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="1c757-114">Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.</span><span class="sxs-lookup"><span data-stu-id="1c757-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="1c757-115">Ne ihtiyacınız var</span><span class="sxs-lookup"><span data-stu-id="1c757-115">What do you need</span></span>
<span data-ttu-id="1c757-116">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c757-116">You must have successfully completed:</span></span>
- <span data-ttu-id="1c757-117">[Arduino panonuzu ile çalışmaya başlama][get-started]</span><span class="sxs-lookup"><span data-stu-id="1c757-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="1c757-118">[Azure IOT hub'ınızı oluşturma][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="1c757-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="1c757-119">Açık hello örnek uygulaması</span><span class="sxs-lookup"><span data-stu-id="1c757-119">Open hello sample app</span></span>
<span data-ttu-id="1c757-120">Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:</span><span class="sxs-lookup"><span data-stu-id="1c757-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* <span data-ttu-id="1c757-122">Merhaba `app.ino` hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="1c757-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="1c757-123">Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.</span><span class="sxs-lookup"><span data-stu-id="1c757-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="1c757-124">Merhaba `config.json` gerekli yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c757-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="1c757-125">Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="1c757-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="1c757-126">Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="1c757-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="1c757-127">Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="1c757-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="1c757-128">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c757-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="1c757-129">Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="1c757-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri][arm-template-params]

* <span data-ttu-id="1c757-131">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Arduino panonuzu kayıtlı] [ created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="1c757-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="1c757-132">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="1c757-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="1c757-133">Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c757-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="1c757-134">Bir çizgi ya da rakamla hello önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1c757-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="1c757-135">Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:</span><span class="sxs-lookup"><span data-stu-id="1c757-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="1c757-136">Bu kaynakları toocreate yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="1c757-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="1c757-137">Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c757-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="1c757-138">Özet</span><span class="sxs-lookup"><span data-stu-id="1c757-138">Summary</span></span>
<span data-ttu-id="1c757-139">IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler.</span><span class="sxs-lookup"><span data-stu-id="1c757-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="1c757-140">Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Arduino Panonuzda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c757-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c757-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c757-141">Next steps</span></span>
<span data-ttu-id="1c757-142">[Örnek uygulama toosend cihaz bulut iletilerini Arduino Panonuzda çalıştırın.][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="1c757-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md