---
title: "aaaUnderstand hello Azure IOT SDK'ları | Microsoft Docs"
description: "Geliştirici Kılavuzu - hakkında bilgi ve bağlantılar toohello toobuild aygıt uygulamalar ve arka uç uygulamalar kullanabilirsiniz çeşitli Azure IOT cihaz ve hizmet SDK'ları."
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
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="24e1b-103">Anlamak ve Azure IOT SDK'ları kullanın</span><span class="sxs-lookup"><span data-stu-id="24e1b-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="24e1b-104">IOT Hub ile çalışmaya yönelik SDK'ın üç kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="24e1b-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="24e1b-105">**Cihaz SDK'ları** IOT cihazlarınızı üzerinde çalışan toobuild uygulamalar etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="24e1b-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="24e1b-106">Bu uygulamaları tooyour IOT hub'ı telemetri gönderebilir ve isteğe bağlı olarak, IOT hub'ından iletileri alacak.</span><span class="sxs-lookup"><span data-stu-id="24e1b-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="24e1b-107">**Hizmet SDK'ları** , toomanage IOT hub'ınızı etkinleştir ve isteğe bağlı olarak tooyour IOT cihazları iletileri gönder.</span><span class="sxs-lookup"><span data-stu-id="24e1b-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="24e1b-108">**Azure IOT kenar** , kullanmama desteklenen hello protokollerden birini ya da hello kenar tooprocess iletileri gerektiğinde toobuild ağ geçitleri tooenable aygıtları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="24e1b-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="24e1b-109">SDK'ları olan birden fazla programlama dili toosupport sağlanan.</span><span class="sxs-lookup"><span data-stu-id="24e1b-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="24e1b-110">Azure IOT cihaz SDK'ları</span><span class="sxs-lookup"><span data-stu-id="24e1b-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="24e1b-111">Merhaba Microsoft Azure IOT cihaz SDK'ları içeren yapı aygıtları kolaylaştıran kod ve tooand bağlanan uygulamaları Azure IOT Hub Hizmetleri tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="24e1b-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="24e1b-112">Merhaba aşağıdaki Azure IOT cihaz SDK'ları github'dan kullanılabilir toodownload şunlardır:</span><span class="sxs-lookup"><span data-stu-id="24e1b-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="24e1b-113">[C için Azure IOT cihaz SDK'sı] [ lnk-c-device-sdk] taşınabilirlik ve geniş platform uyumluluğu için ANSI C (C99) yazılır.</span><span class="sxs-lookup"><span data-stu-id="24e1b-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="24e1b-114">İki aygıt istemci kitaplığı yok c hello alt düzey **iothub_client** ve hello **seri hale getirici**.</span><span class="sxs-lookup"><span data-stu-id="24e1b-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="24e1b-115">[.NET için Azure IOT cihaz SDK'sı][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="24e1b-116">[Java için Azure IOT cihaz SDK'sı][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="24e1b-117">[Node.js için Azure IOT cihaz SDK'sı][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="24e1b-118">[Python için Azure IOT cihaz SDK'sı][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="24e1b-119">Merhaba readme dosyalarında hello GitHub depolarının dili ve platforma özgü paket yöneticileri tooinstall ikili dosyaları ve bağımlılıkları geliştirme makinenizde kullanma hakkında bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="24e1b-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="24e1b-120">İşletim sistemi platformu ve donanım uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="24e1b-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="24e1b-121">Merhaba belirli donanım aygıtları ile SDK uyumluluğu hakkında daha fazla bilgi için bkz: [Azure IOT cihaz katalog için onaylanmıştır][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="24e1b-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="24e1b-122">Azure IOT hizmeti SDK'ları</span><span class="sxs-lookup"><span data-stu-id="24e1b-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="24e1b-123">Hello Azure IOT hizmeti SDK'ları doğrudan IOT Hub toomanage cihazları ve güvenlik etkileşime uygulamaları derleme kodu toofacilitate içerir.</span><span class="sxs-lookup"><span data-stu-id="24e1b-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="24e1b-124">Merhaba aşağıdaki Azure IOT hizmeti SDK'ları github'dan kullanılabilir toodownload şunlardır:</span><span class="sxs-lookup"><span data-stu-id="24e1b-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="24e1b-125">[.NET için Azure IOT hizmeti SDK'sı][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="24e1b-126">[Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="24e1b-127">[Java için Azure IOT hizmeti SDK'sı][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="24e1b-128">[Python için Azure IOT hizmeti SDK'sı][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="24e1b-129">[C için Azure IOT hizmeti SDK'sı][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="24e1b-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="24e1b-130">Merhaba readme dosyalarında hello GitHub depolarının dili ve platforma özgü paket yöneticileri tooinstall ikili dosyaları ve bağımlılıkları geliştirme makinenizde kullanma hakkında bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="24e1b-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="24e1b-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="24e1b-131">Azure IoT Edge</span></span>

<span data-ttu-id="24e1b-132">Azure IOT kenar hello altyapı ve modülleri toocreate IOT ağ geçidi çözümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="24e1b-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="24e1b-133">IOT kenar toocreate ağ geçitleri uyarlanmış tooany uçtan uca senaryoyu da genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24e1b-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="24e1b-134">İndirebilirsiniz [Azure IOT kenar] [ lnk-iot-edge] github'dan.</span><span class="sxs-lookup"><span data-stu-id="24e1b-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="24e1b-135">Çevrimiçi API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="24e1b-135">Online API reference documentation</span></span>

<span data-ttu-id="24e1b-136">Merhaba aşağıdaki listede bağlantılar tooonline API başvuru belgeleri Azure IOT cihaz, hizmet ve ağ geçidi kitaplıkları içerir:</span><span class="sxs-lookup"><span data-stu-id="24e1b-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="24e1b-137">[Nesnelerin interneti (IOT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="24e1b-138">[IOT hub'ı REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="24e1b-139">[C için Azure IOT cihaz SDK'sı][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="24e1b-140">[Java için Azure IOT cihaz SDK'sı][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="24e1b-141">[Java için Azure IOT hizmeti SDK'sı][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="24e1b-142">[Node.js için Azure IOT cihaz SDK'sı][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="24e1b-143">[Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="24e1b-144">[Azure IOT kenar][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="24e1b-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="24e1b-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24e1b-145">Next steps</span></span>

<span data-ttu-id="24e1b-146">Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="24e1b-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="24e1b-147">[IOT Hub uç noktaları][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="24e1b-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="24e1b-148">[Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="24e1b-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="24e1b-149">[Kotalar ve azaltma][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="24e1b-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="24e1b-150">[IOT Hub MQTT desteği][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="24e1b-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
