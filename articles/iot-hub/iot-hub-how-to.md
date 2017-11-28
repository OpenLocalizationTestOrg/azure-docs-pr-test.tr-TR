---
title: "Azure IOT hub'ı nasıl | Microsoft Docs"
description: "Bir geliştirici olarak, çeşitli IOT Hub özellikleri nasıl kullanırım?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="76c81-103">Azure IOT hub'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="76c81-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="76c81-104">IOT Hub hizmeti için geliştirmeyi öğrenin için çeşitli seçenekleriniz vardır:</span><span class="sxs-lookup"><span data-stu-id="76c81-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="76c81-105">IOT hub'ı özellikleri ayrıntılı açıklamaktadır kavramsal makaleleri okuyun.</span><span class="sxs-lookup"><span data-stu-id="76c81-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="76c81-106">IOT Hub'ın çeşitli özellikleri kapsayan öğreticileri birini izleyin.</span><span class="sxs-lookup"><span data-stu-id="76c81-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="76c81-107">Geliştirici kılavuzu</span><span class="sxs-lookup"><span data-stu-id="76c81-107">Developer guide</span></span>

<span data-ttu-id="76c81-108">Bir geliştirici olarak, IOT Hub hakkında ayrıntılı kavramsal kılavuz okuyabilirsiniz [Geliştirici Kılavuzu][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="76c81-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="76c81-109">Bu kılavuz içerir:</span><span class="sxs-lookup"><span data-stu-id="76c81-109">This guide includes:</span></span>

* <span data-ttu-id="76c81-110">Bunların nasıl kullanılacağını öğrenmek için Yardım tüm IOT hub'ı özelliklerin ayrıntılı açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="76c81-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="76c81-111">Birden çok seçenek kullanılabilir olduğunda seçme hakkında yönergeler.</span><span class="sxs-lookup"><span data-stu-id="76c81-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="76c81-112">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="76c81-112">Tutorials</span></span>

<span data-ttu-id="76c81-113">Uygulama alıştırmalarını aracılığıyla çalışarak belirli IOT hub'ı özellikleri hakkında bilgi edinmek tercih ederseniz, içinden seçim yapabileceğiniz çeşitli eğitim vardır.</span><span class="sxs-lookup"><span data-stu-id="76c81-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="76c81-114">Bu öğreticileri birçoğu, birden fazla programlama dillerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="76c81-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="76c81-115">Bu öğreticiler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="76c81-115">These tutorials include:</span></span>

- <span data-ttu-id="76c81-116">[IOT Hub cihaz-bulut iletileri yolları kullanma][lnk-routes-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="76c81-117">Bu öğretici bir kolay, yapılandırma tabanlı şekilde cihaz bulut iletilerini göndermek için IOT hub'ı yönlendirme kuralları kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="76c81-118">[IOT Hub ile bulut-cihaz iletilerini göndermek][lnk-c2d-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="76c81-119">Bu öğretici, IOT hub'ı aracılığıyla bulut-cihaz iletilerini göndermek ve bulut-cihaz iletilerini bir cihazda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="76c81-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="76c81-120">[IOT Hub ile bulut aygıtlardan dosyaları karşıya yükleme][lnk-upload-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="76c81-121">Bu öğretici, IOT hub'ı dosya karşıya yükleme özelliklerini kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="76c81-122">[Cihaz çiftlerini ile çalışmaya başlama][lnk-twin-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="76c81-123">Bu öğretici cihaz çiftlerini, bildirilen özellikleri, istenen özellikleri ve etiketler için tanıtır.</span><span class="sxs-lookup"><span data-stu-id="76c81-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="76c81-124">Cihaz çiftlerini cihazlarınızı değerleri eşitlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="76c81-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="76c81-125">[Doğrudan yöntemleri kullanın][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="76c81-126">Bu öğretici, doğrudan yöntemlerinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="76c81-127">Sanal cihazınız doğrudan bir yöntem için bir işleyici ekleyin ve IOT hub'ı doğrudan yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="76c81-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="76c81-128">[Aygıt Management'i kullanmaya başlama][lnk-dm-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="76c81-129">Bu öğretici çiftlerini ve doğrudan yöntemleri gibi anahtar cihaz yönetimi özelliklerinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="76c81-130">Sanal cihazınız Uzaktan yeniden başlatmak için bu özellikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="76c81-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="76c81-131">[Cihazları yapılandırmak için istenen özellikleri kullanmak][lnk-properties-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="76c81-132">Bu öğretici nasıl cihazı kullanmak için twin'ın istenen ve özellikleri için uzaktan bildirilen Cihazınızı yapılandırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="76c81-133">[Bir cihaz üretici yazılımı güncelleştirmesi başlatmak için cihaz işleri kullanın][lnk-jobs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="76c81-134">Bu öğretici çiftlerini ve doğrudan yöntemleri gibi anahtar cihaz yönetimi özelliklerinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="76c81-135">Uzaktan aygıtınızın üretici yazılımını güncelleştirmek için bu özellikleri kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="76c81-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="76c81-136">[Zamanlama ve yayın işleri][lnk-schedule-tutorial].</span><span class="sxs-lookup"><span data-stu-id="76c81-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="76c81-137">Bu öğretici, istenen özellikleri ve doğrudan yöntemleri zamanlanmış bir saatte birden çok aygıt ile etkileşim için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="76c81-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76c81-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76c81-138">Next steps</span></span>

<span data-ttu-id="76c81-139">IOT Hub hizmeti hakkında daha fazla bilgi için bkz: [Geliştirici Kılavuzu][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="76c81-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md