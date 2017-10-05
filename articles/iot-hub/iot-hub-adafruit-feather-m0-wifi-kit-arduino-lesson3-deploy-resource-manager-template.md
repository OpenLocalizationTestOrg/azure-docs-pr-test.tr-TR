---
title: "Azure IOT - Ders 3 Connect Arduino (C): şablon dağıtımı | Microsoft Docs"
description: "Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
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
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="6b8e0-104">Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur</span><span class="sxs-lookup"><span data-stu-id="6b8e0-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="6b8e0-105">[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) bulutta.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="6b8e0-106">Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="6b8e0-107">Ne</span><span class="sxs-lookup"><span data-stu-id="6b8e0-107">What will you do</span></span>
<span data-ttu-id="6b8e0-108">Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="6b8e0-109">Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="6b8e0-110">Herhangi bir sorun varsa, çözümleri için Ara [sayfa Adafruit yumuşatma M0 WiFi Arduino panonuz için sorun giderme](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6b8e0-110">If you have any problems, look for solutions on the [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="6b8e0-111">Ne size bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="6b8e0-111">What will you learn</span></span>
<span data-ttu-id="6b8e0-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="6b8e0-112">In this article, you will learn:</span></span>
* <span data-ttu-id="6b8e0-113">Nasıl kullanılacağını [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-113">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="6b8e0-114">IOT hub iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="6b8e0-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="6b8e0-115">Ne ihtiyacınız var</span><span class="sxs-lookup"><span data-stu-id="6b8e0-115">What do you need</span></span>
<span data-ttu-id="6b8e0-116">Başarılı bir şekilde tamamladınız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b8e0-116">You must have successfully completed:</span></span>
- <span data-ttu-id="6b8e0-117">[Arduino panonuzu ile çalışmaya başlama][get-started]</span><span class="sxs-lookup"><span data-stu-id="6b8e0-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="6b8e0-118">[Azure IOT hub'ınızı oluşturma][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="6b8e0-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="6b8e0-119">Örnek uygulamayı açın</span><span class="sxs-lookup"><span data-stu-id="6b8e0-119">Open the sample app</span></span>
<span data-ttu-id="6b8e0-120">Örnek Proje aşağıdaki komutları çalıştırarak Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="6b8e0-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* <span data-ttu-id="6b8e0-122">`app.ino` Dosyasını `app` alt anahtarı kaynağı dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-122">The `app.ino` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="6b8e0-123">Bu kaynak dosyası 20 kez IOT hub'ınıza ileti gönderme ve LED, gönderdiği her ileti için blink kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="6b8e0-124">`config.json` Gerekli yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-124">The `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="6b8e0-125">`arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="6b8e0-126">`arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="6b8e0-127">`ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="6b8e0-128">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b8e0-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="6b8e0-129">Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager şablonu parametreleri][arm-template-params]

* <span data-ttu-id="6b8e0-131">Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Arduino panonuzu kayıtlı] [ created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="6b8e0-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="6b8e0-132">Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="6b8e0-133">Önek, kaynak adı çakışmayı önlemek için genel benzersiz olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="6b8e0-134">Bir çizgi ya da rakamla önekini ilk kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="6b8e0-135">Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:</span><span class="sxs-lookup"><span data-stu-id="6b8e0-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="6b8e0-136">Bu kaynakları oluşturmak için yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="6b8e0-137">Kaynak oluşturma işlemi devam ederken, sonraki makalede hareket ettirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="6b8e0-138">Özet</span><span class="sxs-lookup"><span data-stu-id="6b8e0-138">Summary</span></span>
<span data-ttu-id="6b8e0-139">IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="6b8e0-140">Şimdi, dağıtın ve Arduino Panonuzda cihaz bulut iletilerini göndermek için örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6b8e0-140">You can now deploy and run the sample to send device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b8e0-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b8e0-141">Next steps</span></span>
<span data-ttu-id="6b8e0-142">[Arduino Panonuzda cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="6b8e0-142">[Run a sample application to send device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md