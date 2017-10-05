---
title: "Azure IOT Hub cihaz çiftlerini anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - kullanım cihaz çiftlerini IOT Hub ve aygıtlarınızın arasında durumu ve yapılandırma verileri eşitlemek için"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="53f5d-103">Anlama ve IOT hub'da cihaz çiftlerini kullanın</span><span class="sxs-lookup"><span data-stu-id="53f5d-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="53f5d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="53f5d-104">Overview</span></span>
<span data-ttu-id="53f5d-105">*Cihaz çiftlerini* aygıt durum bilgilerini (meta verileri, yapılandırmaları ve koşullar) depolamak JSON belgeleri.</span><span class="sxs-lookup"><span data-stu-id="53f5d-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="53f5d-106">IoT Hub’ı, IoT Hub'ına bağladığınız her cihaz için bir cihaz çifti sürdürür.</span><span class="sxs-lookup"><span data-stu-id="53f5d-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="53f5d-107">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="53f5d-107">This article describes:</span></span>

* <span data-ttu-id="53f5d-108">Cihaz çifti yapısını: *etiketleri*, *istenen* ve *özellikleri bildirilen*, ve</span><span class="sxs-lookup"><span data-stu-id="53f5d-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="53f5d-109">Cihaz uygulamalarını hem de arka uçları cihaz çiftlerini üzerinde gerçekleştirebileceğiniz işlemler.</span><span class="sxs-lookup"><span data-stu-id="53f5d-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="53f5d-110">Şu anda, cihaz çiftlerini MQTT protokolünü kullanarak IOT hub'a bağlanan cihazlar üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="53f5d-111">Başvurmak [MQTT Destek] [ lnk-devguide-mqtt] MQTT kullanmak mevcut cihaz uygulaması dönüştürme hakkında yönergeler için makalenin.</span><span class="sxs-lookup"><span data-stu-id="53f5d-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="53f5d-112">Kullanılması gereken durumlar</span><span class="sxs-lookup"><span data-stu-id="53f5d-112">When to use</span></span>
<span data-ttu-id="53f5d-113">Cihaz çiftlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="53f5d-113">Use device twins to:</span></span>

* <span data-ttu-id="53f5d-114">Aygıta özgü meta verileri bulutta depolayın.</span><span class="sxs-lookup"><span data-stu-id="53f5d-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="53f5d-115">Örneğin, bir satış makinenin dağıtım konumu.</span><span class="sxs-lookup"><span data-stu-id="53f5d-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="53f5d-116">Rapor geçerli durumu bilgileri kullanılabilir özellikleri ve aygıt uygulamanızdan koşulları gibi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="53f5d-117">Örneğin, bir cihaz IOT hub'ınıza bağlı üzerinden cep telefonu veya WiFi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="53f5d-118">Cihaz uygulaması ve arka uç uygulaması arasında uzun süre çalışan iş akışlarının durumunu eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="53f5d-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="53f5d-119">Örneğin, çözüm yedeklediğinizde yüklemek için yeni üretici yazılımı sürümüne sonunu belirtir ve güncelleştirme işlemi çeşitli aşamaları cihaz uygulaması raporlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="53f5d-120">Cihaz meta verilerini, yapılandırma veya durumu sorgu.</span><span class="sxs-lookup"><span data-stu-id="53f5d-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="53f5d-121">Başvurmak [cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] bildirilen özellikleri, cihaz bulut iletilerini veya karşıya dosya yükleme kullanma konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="53f5d-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="53f5d-122">Başvurmak [bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özellikler, doğrudan yöntemleri veya Bulut-cihaz iletilerini kullanma konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="53f5d-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="53f5d-123">Cihaz çiftlerini</span><span class="sxs-lookup"><span data-stu-id="53f5d-123">Device twins</span></span>
<span data-ttu-id="53f5d-124">Cihaz çiftlerini cihaz ile ilgili bilgileri depolar:</span><span class="sxs-lookup"><span data-stu-id="53f5d-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="53f5d-125">Cihaz ve arka uç aygıtı koşullar ve yapılandırma eşitlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="53f5d-126">Çözüm arka ucu sorgu ve uzun süre çalışan hedef için kullanabileceğiniz işlemleri.</span><span class="sxs-lookup"><span data-stu-id="53f5d-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="53f5d-127">Karşılık gelen cihaz çifti yaşam döngüsü bağlı [cihaz kimliği][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="53f5d-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="53f5d-128">Cihaz çiftlerini örtük olarak oluşturulur ve yeni bir cihaz kimliği oluşturulduğunda veya IOT hub'da silinmiş silinir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="53f5d-129">Cihaz çifti içeren bir JSON belgesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="53f5d-130">**Etiketleri**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-130">**Tags**.</span></span> <span data-ttu-id="53f5d-131">Çözüm arka ucu JSON belgesinin bir bölümünü okuma ve yazma.</span><span class="sxs-lookup"><span data-stu-id="53f5d-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="53f5d-132">Etiketler cihaz uygulamaları için görünür değildir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="53f5d-133">**Özellikler istenen**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-133">**Desired properties**.</span></span> <span data-ttu-id="53f5d-134">Aygıt Yapılandırması veya koşulları eşitlemek için bildirilen özellikleriyle birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="53f5d-135">İstenen özellikler tarafından çözüm arka uç yalnızca ayarlanabilir ve cihaz uygulama tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="53f5d-136">Cihaz uygulaması, gerçek zamanlı istenen özelliklerindeki değişiklikler, aynı zamanda bildirilebilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="53f5d-137">**Özellikler bildirilen**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-137">**Reported properties**.</span></span> <span data-ttu-id="53f5d-138">Aygıt Yapılandırması veya koşulları eşitlemek için istediğiniz özellikleri ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="53f5d-139">Bildirilen özellikleri yalnızca cihaz uygulama tarafından ayarlanabilir ve okunabilir ve çözüm arka ucu tarafından sorgulanan.</span><span class="sxs-lookup"><span data-stu-id="53f5d-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="53f5d-140">Ayrıca, cihaz çifti JSON belgesi kökündeki saklanan karşılık gelen bir cihaz kimliği salt okunur özelliklerinden içeren [kimlik kayıt defteri][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="53f5d-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="53f5d-141">Aşağıdaki örnek, bir cihaz çifti JSON belgesi gösterir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="53f5d-142">Sistem özellikleri kök nesnesinde yer alan ve kapsayıcı nesneleri için `tags` ve her ikisi de `reported` ve `desired` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="53f5d-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="53f5d-143">`properties` Kapsayıcısı bazı salt okunur öğeleri içerir (`$metadata`, `$etag`, ve `$version`) açıklanan [cihaz çifti meta verilerini] [ lnk-twin-metadata] ve [ İyimser eşzamanlılık] [ lnk-concurrency] bölümler.</span><span class="sxs-lookup"><span data-stu-id="53f5d-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="53f5d-144">Bildirilen özelliği örneği</span><span class="sxs-lookup"><span data-stu-id="53f5d-144">Reported property example</span></span>
<span data-ttu-id="53f5d-145">Önceki örnekte, cihaz çifti içeren bir `batteryLevel` cihaz uygulaması tarafından bildirilen özelliği.</span><span class="sxs-lookup"><span data-stu-id="53f5d-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="53f5d-146">Bu özellik, sorgu ve son bildirilen pil düzeyi temelinde cihazlarda çalıştırmak mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="53f5d-147">Cihaz uygulama raporlama cihaz özellikleri veya bağlantı seçenekleri diğer örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="53f5d-148">Bildirilen özellikler çözüm arka ucu bir özelliğin bilinen son değerini nerede ilgilendiği senaryoları basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="53f5d-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="53f5d-149">Kullanım [cihaz bulut iletilerini] [ lnk-d2c] çözüm arka ucu cihaz telemetrisi zaman serisi gibi zaman damgalı olaylar dizisini biçiminde işlemek gerekip gerekmediğini.</span><span class="sxs-lookup"><span data-stu-id="53f5d-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="53f5d-150">İstenen özelliği örneği</span><span class="sxs-lookup"><span data-stu-id="53f5d-150">Desired property example</span></span>
<span data-ttu-id="53f5d-151">Önceki örnekte, `telemetryConfig` cihaz çifti istenen ve bildirilen özellikler çözüm arka ucu ve cihaz uygulaması tarafından bu cihaz için telemetri yapılandırma eşitlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="53f5d-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="53f5d-152">For example:</span></span>

1. <span data-ttu-id="53f5d-153">Çözüm arka ucu istenen özelliği istenen yapılandırma değeri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="53f5d-154">İstenen özellik kümesine sahip belge kısmı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="53f5d-155">Cihaz uygulaması hemen bağlıysa değişiklik ya da ilk yeniden bağlanma sırasında bildirilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="53f5d-156">Cihaz uygulaması güncelleştirilmiş yapılandırmayı daha sonra raporlar (veya bir hata koşulu kullanarak `status` özelliği).</span><span class="sxs-lookup"><span data-stu-id="53f5d-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="53f5d-157">Bildirilen özellikleri kısmı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="53f5d-158">Çözüm arka ucu yapılandırma işleminin sonuçlarını birçok cihaz arasında göre izleyebilirsiniz [sorgulama] [ lnk-query] cihaz çiftlerini.</span><span class="sxs-lookup"><span data-stu-id="53f5d-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="53f5d-159">Önceki kod parçacıkları örnek, bir aygıt yapılandırmasını ve durumunu kodlamak için bir yol okunabilmesi için en iyi duruma getirilmiş verilebilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="53f5d-160">Cihaz çifti istenen ve cihaz çiftlerini özelliklerinde rapor için IOT hub'ı belirli bir şema getirmez.</span><span class="sxs-lookup"><span data-stu-id="53f5d-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="53f5d-161">Bellenim güncelleştirmeleri gibi uzun süre çalışan işlemleri eşitlemek için çiftlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="53f5d-162">Özellikler eşitleyin ve cihaz üzerinden uzun süre çalışan bir işlemi izlemek için nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [kullanmak istediğiniz cihazları yapılandırmak için Özellikler][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="53f5d-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="53f5d-163">Arka plan işlemleri</span><span class="sxs-lookup"><span data-stu-id="53f5d-163">Back-end operations</span></span>
<span data-ttu-id="53f5d-164">Çözüm arka ucu HTTP kullanıma sunulan aşağıdaki atomik işlemleri kullanarak cihaz çifti çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="53f5d-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="53f5d-165">**Cihaz çifti kimliğine göre almak**. İstenen ve etiketler gibi cihaz çifti belge bildirilen, bu işlem döndürür ve Sistem Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="53f5d-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="53f5d-166">**Cihaz çifti kısmen güncelleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-166">**Partially update device twin**.</span></span> <span data-ttu-id="53f5d-167">Bu işlem etiketler veya cihaz çifti istenen özelliklerinde kısmen güncelleştirmek çözüm arka ucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="53f5d-168">Kısmi güncelleştirmeyi ekler veya herhangi bir özellik güncelleştirmeleri bir JSON belgesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="53f5d-169">Özelliklerini ayarlamak `null` kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="53f5d-170">Aşağıdaki örnek yeni bir istenen özellik değeri ile oluşturur `{"newProperty": "newValue"}`, var olan değerini geçersiz kılar `existingProperty` ile `"otherNewValue"`ve kaldırır `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="53f5d-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="53f5d-171">Herhangi bir değişiklik mevcut istenen özellikleri veya etiketleri oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="53f5d-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="53f5d-172">**İstenen Özellikleri Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-172">**Replace desired properties**.</span></span> <span data-ttu-id="53f5d-173">Bu işlem tamamen varolan tüm istenen özellikler üzerine ve yeni bir JSON belgesi için alternatif çözüm arka ucu sağlayan `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="53f5d-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="53f5d-174">**Etiketleri değiştirmek**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-174">**Replace tags**.</span></span> <span data-ttu-id="53f5d-175">Bu işlem tamamen varolan tüm etiketleri üzerine ve yeni bir JSON belgesi için alternatif çözüm arka ucu sağlayan `tags`.</span><span class="sxs-lookup"><span data-stu-id="53f5d-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="53f5d-176">**Twin bildirimlerin**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-176">**Receive twin notifications**.</span></span> <span data-ttu-id="53f5d-177">Bu işlem twin değiştirildiğinde bildirim almak çözüm arka ucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="53f5d-178">Bunu yapmak için IOT çözümünüzün bir rota oluşturmak ve veri kaynağı eşit ayarlamak için gereken *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="53f5d-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="53f5d-179">Varsayılan olarak, hiçbir twin bildirimler gönderilir, diğer bir deyişle, bu tür bir yollar önceden mevcut.</span><span class="sxs-lookup"><span data-stu-id="53f5d-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="53f5d-180">Değişme Oranı çok yüksek ise veya iç hataları gibi başka bir nedenle IOT hub'ı tüm değişiklikleri içeren tek bir bildirim gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="53f5d-181">Uygulamanızı güvenilir denetim ve tüm ara durumlarıyla ilgili günlük gerekiyorsa, bu nedenle, daha sonra hala D2C iletileri kullanan önerilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="53f5d-182">Özellikler ve gövde twin bildirim iletisi içerir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="53f5d-183">Özellikler</span><span class="sxs-lookup"><span data-stu-id="53f5d-183">Properties</span></span>

    | <span data-ttu-id="53f5d-184">Ad</span><span class="sxs-lookup"><span data-stu-id="53f5d-184">Name</span></span> | <span data-ttu-id="53f5d-185">Değer</span><span class="sxs-lookup"><span data-stu-id="53f5d-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="53f5d-186">$content-türü</span><span class="sxs-lookup"><span data-stu-id="53f5d-186">$content-type</span></span> | <span data-ttu-id="53f5d-187">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="53f5d-187">application/json</span></span> |
    <span data-ttu-id="53f5d-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="53f5d-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="53f5d-189">Zaman zaman bildirim gönderildi</span><span class="sxs-lookup"><span data-stu-id="53f5d-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="53f5d-190">$iothub-ileti-kaynak</span><span class="sxs-lookup"><span data-stu-id="53f5d-190">$iothub-message-source</span></span> | <span data-ttu-id="53f5d-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="53f5d-191">twinChangeEvents</span></span> |
    <span data-ttu-id="53f5d-192">$content-kodlama</span><span class="sxs-lookup"><span data-stu-id="53f5d-192">$content-encoding</span></span> | <span data-ttu-id="53f5d-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="53f5d-193">utf-8</span></span> |
    <span data-ttu-id="53f5d-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="53f5d-194">deviceId</span></span> | <span data-ttu-id="53f5d-195">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="53f5d-195">Id of the device</span></span> |
    <span data-ttu-id="53f5d-196">hubName</span><span class="sxs-lookup"><span data-stu-id="53f5d-196">hubName</span></span> | <span data-ttu-id="53f5d-197">IOT hub'ının adı</span><span class="sxs-lookup"><span data-stu-id="53f5d-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="53f5d-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="53f5d-198">operationTimestamp</span></span> | <span data-ttu-id="53f5d-199">[ISO8601] işleminin zaman damgası</span><span class="sxs-lookup"><span data-stu-id="53f5d-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="53f5d-200">ıothub ileti şeması</span><span class="sxs-lookup"><span data-stu-id="53f5d-200">iothub-message-schema</span></span> | <span data-ttu-id="53f5d-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="53f5d-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="53f5d-202">opType</span><span class="sxs-lookup"><span data-stu-id="53f5d-202">opType</span></span> | <span data-ttu-id="53f5d-203">"replaceTwin" veya "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="53f5d-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="53f5d-204">İleti sistemi özelliklerini öneki ile `'$'` simgesi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="53f5d-205">Gövde</span><span class="sxs-lookup"><span data-stu-id="53f5d-205">Body</span></span>
        
    <span data-ttu-id="53f5d-206">Bu bölüm bir JSON biçiminde tüm twin değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="53f5d-207">Bir düzeltme eki aynı biçimi kullanır, farkı olan tüm twin bölümleri içerebilir: etiketleri, properties.reported, properties.desired ve "$metadata" öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="53f5d-208">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="53f5d-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="53f5d-209">Önceki tüm işlemleri destekleyen [iyimser eşzamanlılık] [ lnk-concurrency] ve gerektiren **ServiceConnect** tanımlandığı şekilde izin [güvenlik] [ lnk-security] makalesi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="53f5d-210">Bu işlemlerin yanı sıra çözüm arka ucu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53f5d-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="53f5d-211">SQL benzeri kullanarak cihaz çiftlerini sorgulamak [IOT hub'ı sorgu dili][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="53f5d-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="53f5d-212">Büyük kümelerini kullanarak cihaz çiftlerini işlemleri [işleri][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="53f5d-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="53f5d-213">Aygıt işlemleri</span><span class="sxs-lookup"><span data-stu-id="53f5d-213">Device operations</span></span>
<span data-ttu-id="53f5d-214">Cihaz uygulaması aşağıdaki atomik işlemleri kullanarak cihaz çifti çalışır:</span><span class="sxs-lookup"><span data-stu-id="53f5d-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="53f5d-215">**Cihaz çifti almak**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-215">**Retrieve device twin**.</span></span> <span data-ttu-id="53f5d-216">Bu işlem cihaz çifti belgeyi döndürür (etiketler dahil ve istenen, rapor ve Sistem Özellikleri) şu anda bağlı bir aygıt için.</span><span class="sxs-lookup"><span data-stu-id="53f5d-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="53f5d-217">**Kısmen bildirilen özellikleri güncelleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-217">**Partially update reported properties**.</span></span> <span data-ttu-id="53f5d-218">Bu işlem şu anda bağlı bir aygıt bildirilen özelliklerini kısmi güncelleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="53f5d-219">Bu işlem çözümü istenen özelliklerinin kısmi güncelleştirme son kullanımları geri aynı JSON güncelleştirme biçimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="53f5d-220">**İstenen özelliklerde gözlemlemek**.</span><span class="sxs-lookup"><span data-stu-id="53f5d-220">**Observe desired properties**.</span></span> <span data-ttu-id="53f5d-221">Şu anda bağlı bir aygıt bunlar gerçekleştiğinde istenen özellikleri için güncelleştirmeler bildirilmesini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="53f5d-222">Cihaz çözüm arka ucu tarafından yürütülen Güncelleştirmesi (kısmi veya tam değiştirme) aynı biçiminde alır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="53f5d-223">Önceki tüm işlemleri gerektiren **DeviceConnect** tanımlandığı şekilde izin [güvenlik] [ lnk-security] makalesi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="53f5d-224">[Azure IOT cihaz SDK'ları] [ lnk-sdks] kolaylaştıran birçok diller ve platformlar önceki işlemlerinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="53f5d-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="53f5d-225">İstenen özelliklerde eşitleme için IOT hub'ı elemanlar ayrıntıları hakkında daha fazla bilgi bulunabilir [aygıt yeniden bağlanmayı akış][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="53f5d-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="53f5d-226">Şu anda, cihaz çiftlerini MQTT protokolünü kullanarak IOT hub'a bağlanan cihazlar üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="53f5d-227">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="53f5d-227">Reference topics:</span></span>
<span data-ttu-id="53f5d-228">Aşağıdaki başvuru konuları IOT hub'ınıza erişimini denetleme hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="53f5d-229">Etiketleri ve özellikleri biçimi</span><span class="sxs-lookup"><span data-stu-id="53f5d-229">Tags and properties format</span></span>
<span data-ttu-id="53f5d-230">Etiketler, istenen ve bildirilen özellikleri, aşağıdaki kısıtlamalarla JSON nesneleridir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="53f5d-231">JSON nesnelerinin tüm anahtarları büyük küçük harfe duyarlı 64 baytı UTF-8 UNICODE dizeleri içindedir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="53f5d-232">Karakter hariç UNICODE denetim karakterleri (kesimleri C0 ve C1) izin verilen ve `'.'`, `' '`, ve `'$'`.</span><span class="sxs-lookup"><span data-stu-id="53f5d-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="53f5d-233">JSON nesnelerinin tüm değerleri aşağıdaki JSON türde olabilir: boolean, sayı, dize, nesne.</span><span class="sxs-lookup"><span data-stu-id="53f5d-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="53f5d-234">Diziler izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="53f5d-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="53f5d-235">Etiketler, istenen ve bildirilen özellikleri tüm JSON nesnelerinin maksimum derinliği 5 olabilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="53f5d-236">Örneğin, aşağıdaki nesne geçerli değil:</span><span class="sxs-lookup"><span data-stu-id="53f5d-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="53f5d-237">Tüm dize değerleri en fazla uzunluk olarak 512 baytlık olabilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="53f5d-238">Cihaz çifti boyutu</span><span class="sxs-lookup"><span data-stu-id="53f5d-238">Device twin size</span></span>
<span data-ttu-id="53f5d-239">IOT hub'ı zorlar değerlerine göre bir 8KB boyutu sınırlaması `tags`, `properties/desired`, ve `properties/reported`, salt okunur öğeleri hariç.</span><span class="sxs-lookup"><span data-stu-id="53f5d-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="53f5d-240">Boyutu sayım tarafından UNICODE hariç tüm karakter denetim karakterleri (kesimleri C0 ve C1) ve alan hesaplanır `' '` dışında bir dize sabiti olduğunda görünür.</span><span class="sxs-lookup"><span data-stu-id="53f5d-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="53f5d-241">IOT hub'ı bir hata ile bu belgelerin sınırı üstünde boyutunu artırır tüm işlemleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="53f5d-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="53f5d-242">Cihaz çifti meta veriler</span><span class="sxs-lookup"><span data-stu-id="53f5d-242">Device twin metadata</span></span>
<span data-ttu-id="53f5d-243">IOT Hub cihaz çiftine her bir JSON nesnesi için son güncelleştirme zaman damgası istenen ve Özellikler bildirilen korur.</span><span class="sxs-lookup"><span data-stu-id="53f5d-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="53f5d-244">Zaman damgaları UTC biçimindedir ve kodlanmış [ISO8601] biçimi `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="53f5d-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="53f5d-245">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="53f5d-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="53f5d-246">Bu bilgiler, Nesne anahtarları kaldırmak güncelleştirmeleri korumak için her düzeyde (yalnızca JSON yapısındaki bırakır) tutulur.</span><span class="sxs-lookup"><span data-stu-id="53f5d-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="53f5d-247">İyimser eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="53f5d-247">Optimistic concurrency</span></span>
<span data-ttu-id="53f5d-248">Etiketler, istenen ve tüm destek iyimser eşzamanlılık özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="53f5d-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="53f5d-249">Etiketler göre bir ETag sahip [RFC7232], etiketin JSON gösterimi temsil eden.</span><span class="sxs-lookup"><span data-stu-id="53f5d-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="53f5d-250">Tutarlılık sağlamak için Etag'ler çözüm arka ucu koşullu güncelleştirme işlemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="53f5d-251">Cihaz çifti istenen ve Özellikler rapor Etag'ler gerekmez, ancak sahip bir `$version` artımlı olması garanti değeri.</span><span class="sxs-lookup"><span data-stu-id="53f5d-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="53f5d-252">Benzer şekilde bir ETag öğesine Sürüm güncelleştirme tarafın güncelleştirmeleri tutarlılığı zorlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53f5d-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="53f5d-253">Örneğin, bir cihaz uygulaması bildirilen bir özellik ya da istenen bir özellik için çözüm arka ucu için.</span><span class="sxs-lookup"><span data-stu-id="53f5d-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="53f5d-254">Bir gözlemci Aracı (örneğin, İstenen özelliklerde Gözlemleme cihaz uygulaması) alma işleminin sonucu bir güncelleştirme bildirimi arasındaki diğerleriyle mutabık kılmak sürümleri de yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="53f5d-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="53f5d-255">Bölüm [aygıt yeniden bağlanmayı akış] [ lnk-reconnection] daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="53f5d-256">Cihaz yeniden bağlanmayı akışı</span><span class="sxs-lookup"><span data-stu-id="53f5d-256">Device reconnection flow</span></span>
<span data-ttu-id="53f5d-257">IOT Hub bağlantısı kesilmiş aygıtları için istenen özellikler güncelleştirme bildirimlerini korumaz.</span><span class="sxs-lookup"><span data-stu-id="53f5d-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="53f5d-258">Bu, bağlanan bir aygıt için güncelleştirme bildirimlerini abone yanı sıra tam istenen özellikleri belgenin almanız gerekir izler.</span><span class="sxs-lookup"><span data-stu-id="53f5d-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="53f5d-259">Güncelleştirme bildirimlerini ve tam alma arasında diğerleriyle olasılığını göz önüne alındığında, aşağıdaki akış güvence altına gerekir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="53f5d-260">Cihaz uygulaması bir IOT hub'ına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="53f5d-261">Cihaz uygulaması istenen özelliklerini güncelleştirme bildirimlerini abone olur.</span><span class="sxs-lookup"><span data-stu-id="53f5d-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="53f5d-262">Cihaz uygulamasının tam belgenin istenen özellikleri alır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="53f5d-263">Cihaz uygulaması ile tüm bildirimleri yoksayabilirsiniz `$version` tam alınan belge sürümünden eşit veya daha az.</span><span class="sxs-lookup"><span data-stu-id="53f5d-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="53f5d-264">Bu yaklaşım olası nedeni IOT hub'ı sürümleri her zaman artırmak güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="53f5d-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="53f5d-265">Bu mantık zaten uygulanan [Azure IOT cihaz SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="53f5d-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="53f5d-266">Bu açıklama, yalnızca cihaz uygulaması Azure IOT cihaz SDK'ları hiçbirini kullanamazsınız ve MQTT arabirimi doğrudan program gerekir yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="53f5d-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="53f5d-267">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="53f5d-267">Additional reference material</span></span>
<span data-ttu-id="53f5d-268">IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="53f5d-269">[IOT Hub uç noktaları] [ lnk-endpoints] makalede çeşitli uç noktaları her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="53f5d-270">[Azaltma ve kotaları] [ lnk-quotas] makale IOT Hub hizmeti ve azaltma davranışı hizmetini kullandığınızda beklediğiniz uygulama kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="53f5d-271">[Azure IOT SDK'ları cihazını ve hizmetini] [ lnk-sdks] makale çeşitli dil IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanabilir SDK'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="53f5d-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="53f5d-272">[IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] makalede IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz IOT hub'ı sorgu dili.</span><span class="sxs-lookup"><span data-stu-id="53f5d-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="53f5d-273">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] makale MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f5d-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53f5d-274">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53f5d-274">Next steps</span></span>
<span data-ttu-id="53f5d-275">Şimdi, öğrenilen cihaz çiftlerini hakkında aşağıdaki IOT Hub Geliştirici Kılavuzu konuları ilgilenebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53f5d-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="53f5d-276">[Bir cihazda doğrudan bir yöntem çağırma][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="53f5d-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="53f5d-277">[Birden çok aygıta işleri zamanla][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="53f5d-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="53f5d-278">Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticilerde ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="53f5d-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="53f5d-279">[Cihaz çifti kullanma][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="53f5d-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="53f5d-280">[Cihaz çifti özellikleri kullanma][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="53f5d-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
