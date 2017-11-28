---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: işlev uygulaması oluşturma | Microsoft Docs"
description: "Intel NUC tooyour IOT hub'ından iletileri kaydetmek için tooAzure tablo depolama yazma ve bunları hello buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
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
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="927c0-104">Azure işlev uygulaması ve depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="927c0-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="927c0-105">Azure işlevleri; kolayca çalıştırmak için bir çözüm _işlevleri_ (küçük kod parçalarını) hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="927c0-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="927c0-106">Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="927c0-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="927c0-107">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="927c0-107">What you will do</span></span>

- <span data-ttu-id="927c0-108">Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="927c0-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="927c0-109">Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.</span><span class="sxs-lookup"><span data-stu-id="927c0-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="927c0-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="927c0-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="927c0-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="927c0-111">What you will learn</span></span>

<span data-ttu-id="927c0-112">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="927c0-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="927c0-113">Nasıl toouse Azure Resource Manager toodeploy Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="927c0-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="927c0-114">Nasıl toouse Azure app tooprocess IOT hub'ı iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.</span><span class="sxs-lookup"><span data-stu-id="927c0-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="927c0-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="927c0-115">What you need</span></span>

<span data-ttu-id="927c0-116">Başarılı bir şekilde hello önceki dersleri tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="927c0-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="927c0-117">Ders 1:, Intel NUC IOT ağ geçidi olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="927c0-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="927c0-118">Ders 2: ana bilgisayar ve Azure IOT hub'ı hazırlanın</span><span class="sxs-lookup"><span data-stu-id="927c0-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="927c0-119">Ders 3: SensorTag iletileri almasına ve IOT hub'ından iletileri okur</span><span class="sxs-lookup"><span data-stu-id="927c0-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="927c0-120">Bir örnek uygulamasını açın</span><span class="sxs-lookup"><span data-stu-id="927c0-120">Open a sample app</span></span>

<span data-ttu-id="927c0-121">Tooyour Git `iot-hub-c-intel-nuc-gateway-getting-started` depodaki klasörü, başlatma hello yapılandırma dosyalarını ve Visual Studio Code sonra açık hello örnek proje hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="927c0-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Depodaki yapısı](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="927c0-123">Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="927c0-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="927c0-124">Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="927c0-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="927c0-125">Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="927c0-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="927c0-126">Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="927c0-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="927c0-127">Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.</span><span class="sxs-lookup"><span data-stu-id="927c0-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![ARM şablonu json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="927c0-129">Değiştir `[your IoT Hub name]` ile `{my hub name}` Ders 2'de belirtilen.</span><span class="sxs-lookup"><span data-stu-id="927c0-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="927c0-130">Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:</span><span class="sxs-lookup"><span data-stu-id="927c0-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="927c0-131">Kullanım `iot-gateway` hello değeri olarak `{resource group name}` Ders 2 hello değerinde değiştirilmediyse.</span><span class="sxs-lookup"><span data-stu-id="927c0-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="927c0-132">Özet</span><span class="sxs-lookup"><span data-stu-id="927c0-132">Summary</span></span>

<span data-ttu-id="927c0-133">IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler.</span><span class="sxs-lookup"><span data-stu-id="927c0-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="927c0-134">Şimdi, ağ geçidi tooyour IOT hub tarafından gönderilen iletileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="927c0-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="927c0-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="927c0-135">Next steps</span></span>
<span data-ttu-id="927c0-136">[İletileri okuma Azure Depolama'da kalıcı](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="927c0-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
