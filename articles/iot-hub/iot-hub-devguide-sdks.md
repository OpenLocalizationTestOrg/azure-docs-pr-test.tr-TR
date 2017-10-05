---
title: "Azure IOT SDK'ları anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - ve cihaz uygulamaları ve arka uç uygulamaları oluşturmak için kullanabileceğiniz çeşitli Azure IOT cihaz ve hizmet SDK'lar bağlantılar hakkında bilgi."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="2e96f-103">Anlamak ve Azure IOT SDK'ları kullanın</span><span class="sxs-lookup"><span data-stu-id="2e96f-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="2e96f-104">IOT Hub ile çalışmaya yönelik SDK'ın üç kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="2e96f-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="2e96f-105">**Cihaz SDK'ları** IOT cihazlarınızı üzerinde çalışan uygulamalar geliştirme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e96f-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="2e96f-106">Bu uygulamaları IOT hub'ınıza telemetri göndermek ve isteğe bağlı olarak, IOT hub'ından iletileri alacak.</span><span class="sxs-lookup"><span data-stu-id="2e96f-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="2e96f-107">**Hizmet SDK'ları** IOT hub'ınızı yönetmenize olanak tanıyan ve isteğe bağlı olarak IOT cihazlarınızı ileti gönderin.</span><span class="sxs-lookup"><span data-stu-id="2e96f-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="2e96f-108">**Azure IOT kenar** , kullanmama desteklenen protokollerden birini ya da kenar iletileri işlemek gerektiğinde aygıtları etkinleştirmek için ağ geçitleri oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e96f-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="2e96f-109">SDK'ları, birden fazla programlama dili desteklemek için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2e96f-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="2e96f-110">Azure IOT cihaz SDK'ları</span><span class="sxs-lookup"><span data-stu-id="2e96f-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="2e96f-111">Microsoft Azure IOT cihaz SDK'ları oluşturma aygıtlar ve bağlanmak ve Azure IOT Hub Hizmetleri tarafından yönetilen uygulamalar kolaylaştıran kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="2e96f-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="2e96f-112">Aşağıdaki Azure IOT cihaz SDK'ları Github'dan indirilebilir:</span><span class="sxs-lookup"><span data-stu-id="2e96f-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="2e96f-113">[C için Azure IOT cihaz SDK'sı] [ lnk-c-device-sdk] taşınabilirlik ve geniş platform uyumluluğu için ANSI C (C99) yazılır.</span><span class="sxs-lookup"><span data-stu-id="2e96f-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="2e96f-114">C, alt düzey için iki cihaz istemci Kitaplığı **iothub_client** ve **seri hale getirici**.</span><span class="sxs-lookup"><span data-stu-id="2e96f-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="2e96f-115">[.NET için Azure IOT cihaz SDK'sı][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="2e96f-116">[Java için Azure IOT cihaz SDK'sı][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="2e96f-117">[Node.js için Azure IOT cihaz SDK'sı][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="2e96f-118">[Python için Azure IOT cihaz SDK'sı][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="2e96f-119">GitHub depolarının readme dosyalarında ikili dosyaları ve bağımlılıkları geliştirme makinenizde yüklemek için dil ve platforma özgü paket yöneticileri kullanma hakkında bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="2e96f-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="2e96f-120">İşletim sistemi platformu ve donanım uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="2e96f-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="2e96f-121">Belirli donanım aygıtları ile SDK uyumluluğu hakkında daha fazla bilgi için bkz: [Azure IOT cihaz katalog için onaylanmıştır][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="2e96f-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="2e96f-122">Azure IOT hizmeti SDK'ları</span><span class="sxs-lookup"><span data-stu-id="2e96f-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="2e96f-123">Azure IOT hizmeti SDK'ları cihazları ve güvenliği yönetmek için etkileşime uygulamaları oluşturma IOT Hub ile doğrudan kolaylaştırmak için kod içerir.</span><span class="sxs-lookup"><span data-stu-id="2e96f-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="2e96f-124">Aşağıdaki Azure IOT hizmeti SDK'ları Github'dan indirilebilir:</span><span class="sxs-lookup"><span data-stu-id="2e96f-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="2e96f-125">[.NET için Azure IOT hizmeti SDK'sı][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="2e96f-126">[Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="2e96f-127">[Java için Azure IOT hizmeti SDK'sı][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="2e96f-128">[Python için Azure IOT hizmeti SDK'sı][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="2e96f-129">[C için Azure IOT hizmeti SDK'sı][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="2e96f-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="2e96f-130">GitHub depolarının readme dosyalarında ikili dosyaları ve bağımlılıkları geliştirme makinenizde yüklemek için dil ve platforma özgü paket yöneticileri kullanma hakkında bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="2e96f-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="2e96f-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="2e96f-131">Azure IoT Edge</span></span>

<span data-ttu-id="2e96f-132">Azure IOT kenar altyapısı ve IOT ağ geçidi çözümler oluşturmak için modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="2e96f-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="2e96f-133">IOT bir uçtan uca senaryonuz için özel olarak hazırlanmış ağ geçitleri oluşturmak için kenar genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e96f-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="2e96f-134">İndirebilirsiniz [Azure IOT kenar] [ lnk-iot-edge] github'dan.</span><span class="sxs-lookup"><span data-stu-id="2e96f-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="2e96f-135">Çevrimiçi API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="2e96f-135">Online API reference documentation</span></span>

<span data-ttu-id="2e96f-136">Aşağıdaki liste, Azure IOT cihaz, hizmet ve ağ geçidi kitaplıkları için çevrimiçi API başvuru belgeleri bağlantılarını içerir:</span><span class="sxs-lookup"><span data-stu-id="2e96f-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="2e96f-137">[Nesnelerin interneti (IOT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="2e96f-138">[IOT hub'ı REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="2e96f-139">[C için Azure IOT cihaz SDK'sı][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="2e96f-140">[Java için Azure IOT cihaz SDK'sı][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="2e96f-141">[Java için Azure IOT hizmeti SDK'sı][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="2e96f-142">[Node.js için Azure IOT cihaz SDK'sı][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="2e96f-143">[Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="2e96f-144">[Azure IOT kenar][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="2e96f-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e96f-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e96f-145">Next steps</span></span>

<span data-ttu-id="2e96f-146">Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="2e96f-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2e96f-147">[IOT Hub uç noktaları][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="2e96f-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="2e96f-148">[Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="2e96f-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="2e96f-149">[Kotalar ve azaltma][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="2e96f-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="2e96f-150">[IOT Hub MQTT desteği][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="2e96f-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
