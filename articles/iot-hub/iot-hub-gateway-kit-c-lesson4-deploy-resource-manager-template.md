---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: işlev uygulaması oluşturma | Microsoft Docs"
description: "IOT hub'ınıza Intel NUC iletileri kaydetmek için bunları Azure Table depolama alanına yazmak ve bunları buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="1564b-104">Azure işlev uygulaması ve depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1564b-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="1564b-105">Azure işlevleri; kolayca çalıştırmak için bir çözüm _işlevleri_ (küçük kod parçalarını) bulutta.</span><span class="sxs-lookup"><span data-stu-id="1564b-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="1564b-106">Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="1564b-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="1564b-107">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="1564b-107">What you will do</span></span>

- <span data-ttu-id="1564b-108">Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1564b-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="1564b-109">Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.</span><span class="sxs-lookup"><span data-stu-id="1564b-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="1564b-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1564b-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="1564b-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="1564b-111">What you will learn</span></span>

<span data-ttu-id="1564b-112">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1564b-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="1564b-113">Azure Resource Manager Azure kaynaklarınızı dağıtmak için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="1564b-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="1564b-114">IOT hub'ı iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="1564b-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1564b-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="1564b-115">What you need</span></span>

<span data-ttu-id="1564b-116">Başarıyla önceki dersleri tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1564b-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="1564b-117">Ders 1:, Intel NUC IOT ağ geçidi olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="1564b-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="1564b-118">Ders 2: ana bilgisayar ve Azure IOT hub'ı hazırlanın</span><span class="sxs-lookup"><span data-stu-id="1564b-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="1564b-119">Ders 3: SensorTag iletileri almasına ve IOT hub'ından iletileri okur</span><span class="sxs-lookup"><span data-stu-id="1564b-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="1564b-120">Bir örnek uygulamasını açın</span><span class="sxs-lookup"><span data-stu-id="1564b-120">Open a sample app</span></span>

<span data-ttu-id="1564b-121">Gidin, `iot-hub-c-intel-nuc-gateway-getting-started` deposu klasör, yapılandırma dosyalarını başlatın ve aşağıdaki komutu çalıştırarak bu örnek proje Visual Studio kodda açın:</span><span class="sxs-lookup"><span data-stu-id="1564b-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Depodaki yapısı](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="1564b-123">`arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="1564b-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="1564b-124">`arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="1564b-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="1564b-125">`ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="1564b-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="1564b-126">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="1564b-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="1564b-127">Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="1564b-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![ARM şablonu json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="1564b-129">Değiştir `[your IoT Hub name]` ile `{my hub name}` Ders 2'de belirtilen.</span><span class="sxs-lookup"><span data-stu-id="1564b-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="1564b-130">Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:</span><span class="sxs-lookup"><span data-stu-id="1564b-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="1564b-131">Kullanım `iot-gateway` değeri olarak `{resource group name}` Ders 2 değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="1564b-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="1564b-132">Özet</span><span class="sxs-lookup"><span data-stu-id="1564b-132">Summary</span></span>

<span data-ttu-id="1564b-133">IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1564b-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="1564b-134">Şimdi, ağ geçidi IOT hub'ınıza gönderdiği iletileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="1564b-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1564b-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1564b-135">Next steps</span></span>
<span data-ttu-id="1564b-136">[İletileri okuma Azure Depolama'da kalıcı](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1564b-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
