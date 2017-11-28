---
title: "aaaUnderstand Azure IOT Hub cihaz çiftlerini | Microsoft Docs"
description: "Geliştirici Kılavuzu - kullanım cihaz IOT Hub ve aygıtlarınızın arasında toosynchronize durumu ve yapılandırma verileri çiftlerini"
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="4ef3c-103">Anlama ve IOT hub'da cihaz çiftlerini kullanın</span><span class="sxs-lookup"><span data-stu-id="4ef3c-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="4ef3c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4ef3c-104">Overview</span></span>
<span data-ttu-id="4ef3c-105">*Cihaz çiftlerini* aygıt durum bilgilerini (meta verileri, yapılandırmaları ve koşullar) depolamak JSON belgeleri.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="4ef3c-106">IOT Hub cihaz çifti tooIoT Hub bağlanmak her aygıt için devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="4ef3c-107">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-107">This article describes:</span></span>

* <span data-ttu-id="4ef3c-108">Merhaba hello cihaz çifti yapısını: *etiketleri*, *istenen* ve *özellikleri bildirilen*, ve</span><span class="sxs-lookup"><span data-stu-id="4ef3c-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="4ef3c-109">cihaz çiftlerini cihaz uygulamalarını hem de arka uçları gerçekleştirebilirsiniz hello işlemleri.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="4ef3c-110">Şu anda, cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="4ef3c-111">Toohello başvuran [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="4ef3c-112">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="4ef3c-112">When toouse</span></span>
<span data-ttu-id="4ef3c-113">Cihaz çiftlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-113">Use device twins to:</span></span>

* <span data-ttu-id="4ef3c-114">Aygıta özgü meta veriler hello bulutta depolayın.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="4ef3c-115">Örneğin, bir satış makinenin dağıtım konumu hello.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="4ef3c-116">Rapor geçerli durumu bilgileri kullanılabilir özellikleri ve aygıt uygulamanızdan koşulları gibi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="4ef3c-117">Örneğin, bir cihaz bağlı tooyour IOT hub, cep telefonu üzerinden veya WiFi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="4ef3c-118">Uzun süre çalışan iş akışları cihaz uygulaması ve arka uç uygulaması arasında Hello durumunu eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="4ef3c-119">Örneğin, Hello çözüm yedeklediğinizde son yeni bellenim sürümü tooinstall hello ve hello cihaz uygulama raporları hello güncelleştirme işleminin çeşitli aşamaları hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="4ef3c-120">Cihaz meta verilerini, yapılandırma veya durumu sorgu.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="4ef3c-121">Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] bildirilen özellikleri, cihaz bulut iletilerini veya karşıya dosya yükleme kullanma konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="4ef3c-122">Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özellikler, doğrudan yöntemleri veya Bulut-cihaz iletilerini kullanma konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="4ef3c-123">Cihaz çiftlerini</span><span class="sxs-lookup"><span data-stu-id="4ef3c-123">Device twins</span></span>
<span data-ttu-id="4ef3c-124">Cihaz çiftlerini cihaz ile ilgili bilgileri depolar:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="4ef3c-125">Cihaz ve arka uç toosynchronize aygıt koşullar ve yapılandırma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="4ef3c-126">Merhaba çözüm arka ucu tooquery ve uzun süre çalışan işlemleri hedef kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="4ef3c-127">cihaz çifti Hello yaşam döngüsü bağlı toohello karşılık gelen [cihaz kimliği][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="4ef3c-128">Cihaz çiftlerini örtük olarak oluşturulur ve yeni bir cihaz kimliği oluşturulduğunda veya IOT hub'da silinmiş silinir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="4ef3c-129">Cihaz çifti içeren bir JSON belgesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="4ef3c-130">**Etiketleri**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-130">**Tags**.</span></span> <span data-ttu-id="4ef3c-131">Çözüm arka ucu hello hello JSON belgesinin bir bölümünü okuma ve yazma.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="4ef3c-132">Etiketler görünür toodevice uygulamalar olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="4ef3c-133">**Özellikler istenen**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-133">**Desired properties**.</span></span> <span data-ttu-id="4ef3c-134">Bildirilen özellikleri toosynchronize aygıt yapılandırması veya koşulları ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="4ef3c-135">İstenen özellikler yalnızca hello çözüm tarafından arka uç ayarlayabilirsiniz ve hello cihaz uygulama tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="4ef3c-136">Merhaba cihaz uygulaması, gerçek zamanlı istenen hello özelliklerindeki değişiklikler de bildirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="4ef3c-137">**Özellikler bildirilen**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-137">**Reported properties**.</span></span> <span data-ttu-id="4ef3c-138">İstenen özelliklerde toosynchronize aygıt yapılandırması veya koşulları ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="4ef3c-139">Bildirilen özellikleri yalnızca hello cihaz uygulama tarafından ayarlanabilir ve okunabilir ve hello çözüm arka ucu tarafından sorgulanan.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="4ef3c-140">Ayrıca, hello salt okunur özellikler hello hello saklanan karşılık gelen cihaz Kimliği'hello hello cihaz çifti JSON belgesi kökündeki içeren [kimlik kayıt defteri][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="4ef3c-141">Aşağıdaki örnek hello cihaz çifti JSON belgesi gösterir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="4ef3c-142">Merhaba kök nesnesindeki hello sistem özelliklerdir ve kapsayıcı nesneleri için `tags` ve her ikisi de `reported` ve `desired` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="4ef3c-143">Merhaba `properties` kapsayıcısı bazı salt okunur öğeleri içerir (`$metadata`, `$etag`, ve `$version`) hello açıklanan [cihaz çifti meta verilerini] [ lnk-twin-metadata] ve [ İyimser eşzamanlılık] [ lnk-concurrency] bölümler.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="4ef3c-144">Bildirilen özelliği örneği</span><span class="sxs-lookup"><span data-stu-id="4ef3c-144">Reported property example</span></span>
<span data-ttu-id="4ef3c-145">Merhaba önceki örnekte hello cihaz çifti içeren bir `batteryLevel` hello cihaz uygulaması tarafından bildirilen özelliği.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="4ef3c-146">Bu özellik, olası tooquery kolaylaştırır ve hello son bildirilen pil düzeyi temelinde cihazlarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="4ef3c-147">Merhaba cihaz uygulama raporlama cihaz özellikleri veya bağlantı seçenekleri diğer örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="4ef3c-148">Bildirilen özellikleri hello çözüm arka ucu bir özelliğin değerini bilinen son hello burada ilgilendiği senaryoları basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="4ef3c-149">Kullanım [cihaz bulut iletilerini] [ lnk-d2c] hello çözüm arka ucu tooprocess cihaz telemetrisi zaman serisi gibi zaman damgalı olaylar dizisini hello biçiminde gerekip gerekmediğini.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="4ef3c-150">İstenen özelliği örneği</span><span class="sxs-lookup"><span data-stu-id="4ef3c-150">Desired property example</span></span>
<span data-ttu-id="4ef3c-151">Merhaba önceki örnekte hello `telemetryConfig` cihaz çifti istenen ve bildirilen özellikleri hello çözüm arka ucu ve hello aygıt uygulama toosynchronize hello telemetri yapılandırması tarafından bu aygıt için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="4ef3c-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-152">For example:</span></span>

1. <span data-ttu-id="4ef3c-153">Hello çözüm arka ucu istenen hello özelliğiyle istenen hello yapılandırma değeri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="4ef3c-154">İstenen hello özellik kümesi hello belgeyle hello kısmı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="4ef3c-155">Merhaba cihaz uygulaması hemen bağlı veya hello ilk yeniden hello değişikliği bildirilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="4ef3c-156">Merhaba cihaz uygulamasının daha sonra güncelleştirilen hello yapılandırma raporlar (veya hello kullanarak bir hata koşulu `status` özelliği).</span><span class="sxs-lookup"><span data-stu-id="4ef3c-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="4ef3c-157">İşte hello hello kısmı bildirilen özellikleri:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="4ef3c-158">Merhaba çözüm arka ucu izleyebilirsiniz hello yapılandırma işlemi hello sonuçlarını birçok cihaz arasında göre [sorgulama] [ lnk-query] cihaz çiftlerini.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="4ef3c-159">Merhaba önceki kod parçacıkları, örnekler bir aygıt yapılandırmasını ve durumunu bir yolu tooencode okunabilmesi için en iyi duruma getirilmiş.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="4ef3c-160">Merhaba cihaz çifti istenen ve hello cihaz çiftlerini özelliklerinde rapor için IOT hub'ı belirli bir şema getirmez.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="4ef3c-161">Bellenim güncelleştirmeleri gibi çiftlerini toosynchronize uzun süre çalışan işlemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="4ef3c-162">Nasıl bkz: toouse özellikleri toosynchronize ve cihazlarda, uzun süre çalışan işlemin izleme hakkında daha fazla bilgi için [kullanım istenen özellikleri tooconfigure aygıtları][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="4ef3c-163">Arka plan işlemleri</span><span class="sxs-lookup"><span data-stu-id="4ef3c-163">Back-end operations</span></span>
<span data-ttu-id="4ef3c-164">Merhaba çözüm arka ucu hello cihaz çifti atomik işlemleri, HTTP kullanıma sunulan aşağıdaki hello kullanarak çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="4ef3c-165">**Cihaz çifti kimliğine göre almak**. Etiketler dahil ve istenen, hello cihaz çifti belge bildirilen, bu işlem döndürür ve Sistem Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="4ef3c-166">**Cihaz çifti kısmen güncelleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-166">**Partially update device twin**.</span></span> <span data-ttu-id="4ef3c-167">Bu işlem hello çözüm arka ucu toopartially güncelleştirme hello etiket veya cihaz çiftine istenen özellikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="4ef3c-168">Merhaba kısmi güncelleştirme ekler veya herhangi bir özellik güncelleştirmeleri bir JSON belgesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="4ef3c-169">Çok ayarlanan özellikleri`null` kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="4ef3c-170">Merhaba aşağıdaki örnek yeni bir istenen özellik değeri ile oluşturur `{"newProperty": "newValue"}`, hello varolan değerini geçersiz kılar `existingProperty` ile `"otherNewValue"`ve kaldırır `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="4ef3c-171">Başka değişiklik istenen tooexisting özellikleri veya etiketleri oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="4ef3c-172">**İstenen Özellikleri Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-172">**Replace desired properties**.</span></span> <span data-ttu-id="4ef3c-173">Bu işlemi etkinleştirir hello çözüm arka ucu toocompletely tüm mevcut istenen özellikleri üzerine ve yeni bir JSON belgesi için alternatif `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="4ef3c-174">**Etiketleri değiştirmek**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-174">**Replace tags**.</span></span> <span data-ttu-id="4ef3c-175">Bu işlemi etkinleştirir hello çözüm arka ucu toocompletely tüm varolan etiketleri üzerine ve yeni bir JSON belgesi için alternatif `tags`.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="4ef3c-176">**Twin bildirimlerin**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-176">**Receive twin notifications**.</span></span> <span data-ttu-id="4ef3c-177">Bu işlem hello çözüm arka ucu toobe hello twin değiştirildiğinde bildirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="4ef3c-178">toodo bu nedenle, IOT çözümünüzü toocreate bir yol ve tooset hello veri kaynağı eşittir çok gereken*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="4ef3c-179">Varsayılan olarak, hiçbir twin bildirimler gönderilir, diğer bir deyişle, bu tür bir yollar önceden mevcut.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="4ef3c-180">Merhaba değişme oranı çok yüksek ise veya iç hataları gibi başka bir nedenle hello IOT hub'ı tüm değişiklikleri içeren tek bir bildirim gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="4ef3c-181">Uygulamanızı güvenilir denetim ve tüm ara durumlarıyla ilgili günlük gerekiyorsa, bu nedenle, daha sonra hala D2C iletileri kullanan önerilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="4ef3c-182">Merhaba twin bildirim iletisi özelliklerini ve gövde içerir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="4ef3c-183">Özellikler</span><span class="sxs-lookup"><span data-stu-id="4ef3c-183">Properties</span></span>

    | <span data-ttu-id="4ef3c-184">Ad</span><span class="sxs-lookup"><span data-stu-id="4ef3c-184">Name</span></span> | <span data-ttu-id="4ef3c-185">Değer</span><span class="sxs-lookup"><span data-stu-id="4ef3c-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="4ef3c-186">$content-türü</span><span class="sxs-lookup"><span data-stu-id="4ef3c-186">$content-type</span></span> | <span data-ttu-id="4ef3c-187">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="4ef3c-187">application/json</span></span> |
    <span data-ttu-id="4ef3c-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="4ef3c-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="4ef3c-189">Zaman zaman hello bildirim gönderildi</span><span class="sxs-lookup"><span data-stu-id="4ef3c-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="4ef3c-190">$iothub-ileti-kaynak</span><span class="sxs-lookup"><span data-stu-id="4ef3c-190">$iothub-message-source</span></span> | <span data-ttu-id="4ef3c-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="4ef3c-191">twinChangeEvents</span></span> |
    <span data-ttu-id="4ef3c-192">$content-kodlama</span><span class="sxs-lookup"><span data-stu-id="4ef3c-192">$content-encoding</span></span> | <span data-ttu-id="4ef3c-193">UTF-8</span><span class="sxs-lookup"><span data-stu-id="4ef3c-193">utf-8</span></span> |
    <span data-ttu-id="4ef3c-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="4ef3c-194">deviceId</span></span> | <span data-ttu-id="4ef3c-195">Merhaba aygıtın kimliği</span><span class="sxs-lookup"><span data-stu-id="4ef3c-195">Id of hello device</span></span> |
    <span data-ttu-id="4ef3c-196">hubName</span><span class="sxs-lookup"><span data-stu-id="4ef3c-196">hubName</span></span> | <span data-ttu-id="4ef3c-197">IOT hub'ının adı</span><span class="sxs-lookup"><span data-stu-id="4ef3c-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="4ef3c-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="4ef3c-198">operationTimestamp</span></span> | <span data-ttu-id="4ef3c-199">[ISO8601] işleminin zaman damgası</span><span class="sxs-lookup"><span data-stu-id="4ef3c-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="4ef3c-200">ıothub ileti şeması</span><span class="sxs-lookup"><span data-stu-id="4ef3c-200">iothub-message-schema</span></span> | <span data-ttu-id="4ef3c-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="4ef3c-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="4ef3c-202">opType</span><span class="sxs-lookup"><span data-stu-id="4ef3c-202">opType</span></span> | <span data-ttu-id="4ef3c-203">"replaceTwin" veya "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="4ef3c-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="4ef3c-204">İleti sistemi özellikleri ile Merhaba önekli `'$'` simgesi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="4ef3c-205">Gövde</span><span class="sxs-lookup"><span data-stu-id="4ef3c-205">Body</span></span>
        
    <span data-ttu-id="4ef3c-206">Bu bölüm bir JSON biçiminde tüm hello twin değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="4ef3c-207">Bir düzeltme eki hello aynı biçimi kullanır, hello farkı olan tüm twin bölümleri içerebilir: etiketleri, properties.reported, properties.desired ve hello "$metadata" öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="4ef3c-208">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="4ef3c-208">For example,</span></span>
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

<span data-ttu-id="4ef3c-209">Tüm önceki operations desteği hello [iyimser eşzamanlılık] [ lnk-concurrency] ve hello gerektiren **ServiceConnect** hello tanımlanan izin [güvenlik ] [ lnk-security] makalesi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="4ef3c-210">Ayrıca son can toothese işlemleri, hello çözüm arka:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="4ef3c-211">Sorgu hello kullanarak hello cihaz çiftlerini SQL benzeri [IOT hub'ı sorgu dili][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="4ef3c-212">Büyük kümelerini kullanarak cihaz çiftlerini işlemleri [işleri][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="4ef3c-213">Aygıt işlemleri</span><span class="sxs-lookup"><span data-stu-id="4ef3c-213">Device operations</span></span>
<span data-ttu-id="4ef3c-214">Merhaba cihaz uygulaması atomik işlemleri aşağıdaki hello kullanarak hello cihaz çifti üzerinde çalışır:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="4ef3c-215">**Cihaz çifti almak**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-215">**Retrieve device twin**.</span></span> <span data-ttu-id="4ef3c-216">Bu işlem hello cihaz çifti belgeyi döndürür (etiketler dahil ve istenen, rapor ve Sistem Özellikleri) hello cihaz şu anda bağlı.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="4ef3c-217">**Kısmen bildirilen özellikleri güncelleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-217">**Partially update reported properties**.</span></span> <span data-ttu-id="4ef3c-218">Bu işlemi etkinleştirir hello kısmi güncelleştirilmesini hello hello şu anda bağlı cihaz özelliklerini bildirdi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="4ef3c-219">Aynı JSON güncelleştirme bu işlemi kullanan hello hello çözüm arka uç kullanan istenen özelliklerinin kısmi bir güncelleştirme için biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="4ef3c-220">**İstenen özelliklerde gözlemlemek**.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-220">**Observe desired properties**.</span></span> <span data-ttu-id="4ef3c-221">Merhaba şu anda bağlı cihaz gerçekleşmeden güncelleştirmeleri istenen toohello özelliklerini bildirim toobe seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="4ef3c-222">Merhaba aygıt güncelleştirme (kısmi veya tam değiştirme) aynı biçiminde hello çözüm arka ucu tarafından yürütülen hello alır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="4ef3c-223">Tüm önceki işlemleri hello hello gerektiren **DeviceConnect** hello tanımlanan izin [güvenlik] [ lnk-security] makalesi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="4ef3c-224">Merhaba [Azure IOT cihaz SDK'ları] [ lnk-sdks] birçok diller ve platformlar işlemlerinden önceki kolay toouse hello kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="4ef3c-225">İstenen özelliklerde eşitleme için IOT hub'ı elemanlar hello ayrıntıları hakkında daha fazla bilgi bulunabilir [aygıt yeniden bağlanmayı akış][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="4ef3c-226">Şu anda, cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="4ef3c-227">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-227">Reference topics:</span></span>
<span data-ttu-id="4ef3c-228">Merhaba aşağıdaki başvuru konuları denetleme erişim tooyour IOT hub'ı hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="4ef3c-229">Etiketleri ve özellikleri biçimi</span><span class="sxs-lookup"><span data-stu-id="4ef3c-229">Tags and properties format</span></span>
<span data-ttu-id="4ef3c-230">Etiketler, istenen ve bildirilen özellikleri hello kısıtlamaları aşağıdaki JSON nesneleridir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="4ef3c-231">JSON nesnelerinin tüm anahtarları büyük küçük harfe duyarlı 64 baytı UTF-8 UNICODE dizeleri içindedir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="4ef3c-232">Karakter hariç UNICODE denetim karakterleri (kesimleri C0 ve C1) izin verilen ve `'.'`, `' '`, ve `'$'`.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="4ef3c-233">JSON nesnelerinin tüm değerleri şu JSON türlerini hello olabilir: boolean, sayı, dize, nesne.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="4ef3c-234">Diziler izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="4ef3c-235">Etiketler, istenen ve bildirilen özellikleri tüm JSON nesnelerinin maksimum derinliği 5 olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="4ef3c-236">Örneğin, nesne aşağıdaki hello geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="4ef3c-237">Tüm dize değerleri en fazla uzunluk olarak 512 baytlık olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="4ef3c-238">Cihaz çifti boyutu</span><span class="sxs-lookup"><span data-stu-id="4ef3c-238">Device twin size</span></span>
<span data-ttu-id="4ef3c-239">IOT hub'ı zorlayan bir 8KB boyutu sınırlaması hello değerleri `tags`, `properties/desired`, ve `properties/reported`, salt okunur öğeleri hariç.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="4ef3c-240">Merhaba boyutu sayım tarafından UNICODE hariç tüm karakter denetim karakterleri (kesimleri C0 ve C1) ve alan hesaplanır `' '` dışında bir dize sabiti olduğunda görünür.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="4ef3c-241">IOT hub'ı bir hata ile bu belgelerin hello sınırı üstünde hello boyutunu artırır tüm işlemleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="4ef3c-242">Cihaz çifti meta veriler</span><span class="sxs-lookup"><span data-stu-id="4ef3c-242">Device twin metadata</span></span>
<span data-ttu-id="4ef3c-243">IOT Hub cihaz çifti her JSON nesnesinde son güncelleştirmesi hello hello zaman damgası istenen ve Özellikler bildirilen korur.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="4ef3c-244">Merhaba zaman damgaları UTC biçimindedir ve hello kodlanmış [ISO8601] biçimi `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="4ef3c-245">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-245">For example:</span></span>

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

<span data-ttu-id="4ef3c-246">Bu bilgiler Nesne anahtarları kaldıran her düzey (Merhaba JSON yapısı, yalnızca hello bırakır) toopreserve güncelleştirmeleri tutulur.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="4ef3c-247">İyimser eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="4ef3c-247">Optimistic concurrency</span></span>
<span data-ttu-id="4ef3c-248">Etiketler, istenen ve tüm destek iyimser eşzamanlılık özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="4ef3c-249">Etiketler göre bir ETag sahip [RFC7232], hello etiketinin JSON gösterimi temsil eden.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="4ef3c-250">Etag'ler hello çözüm arka ucu tooensure tutarlılık koşullu güncelleştirme işlemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="4ef3c-251">Cihaz çifti istenen ve Özellikler rapor Etag'ler gerekmez, ancak sahip bir `$version` toobe artımlı garanti değeri.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="4ef3c-252">Benzer şekilde tooan ETag, hello sürüm güncelleştirmelerini taraf tooenforce tutarlılığı güncelleştirme hello tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="4ef3c-253">Örneğin, bir cihaz uygulaması için bir bildirilen özelliği veya hello çözüm arka ucu istenen bir özellik için.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="4ef3c-254">Bir gözlemci Aracı (örneğin, istenen hello özellikleri Gözlemleme hello cihaz uygulaması) alma işleminin hello sonucu bir güncelleştirme bildirimi arasındaki diğerleriyle mutabık kılmak sürümleri de yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="4ef3c-255">Merhaba bölüm [aygıt yeniden bağlanmayı akış] [ lnk-reconnection] daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="4ef3c-256">Cihaz yeniden bağlanmayı akışı</span><span class="sxs-lookup"><span data-stu-id="4ef3c-256">Device reconnection flow</span></span>
<span data-ttu-id="4ef3c-257">IOT Hub bağlantısı kesilmiş aygıtları için istenen özellikler güncelleştirme bildirimlerini korumaz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="4ef3c-258">Bu güncelleştirme bildirimlerini toplama toosubscribing de hello tam istenen özellikler belgesinde bağlanan bir aygıt almanız gerekir izler.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="4ef3c-259">Güncelleştirme bildirimlerini ve tam alma arasında diğerleriyle Hello olasılığını göz önüne alındığında, akış aşağıdaki hello güvence altına gerekir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="4ef3c-260">Cihaz uygulaması tooan IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="4ef3c-261">Cihaz uygulaması istenen özelliklerini güncelleştirme bildirimlerini abone olur.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="4ef3c-262">Cihaz uygulaması hello tam belge istenen özellikleri alır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="4ef3c-263">Merhaba cihaz uygulaması ile tüm bildirimleri yoksayabilirsiniz `$version` hello tam alınan belge hello sürümünden eşit veya daha az.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="4ef3c-264">Bu yaklaşım olası nedeni IOT hub'ı sürümleri her zaman artırmak güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="4ef3c-265">Bu mantık hello zaten uygulanmış [Azure IOT cihaz SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="4ef3c-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="4ef3c-266">Bu açıklama hello cihaz uygulaması Azure IOT cihaz SDK'ları hiçbirini kullanamazsınız ve hello MQTT arabirimi doğrudan program gerekir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="4ef3c-267">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="4ef3c-267">Additional reference material</span></span>
<span data-ttu-id="4ef3c-268">Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4ef3c-269">Merhaba [IOT Hub uç noktaları] [ lnk-endpoints] makalede hello çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4ef3c-270">Merhaba [azaltma ve kotaları] [ lnk-quotas] makale toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="4ef3c-271">Merhaba [Azure IOT SDK'ları cihazını ve hizmetini] [ lnk-sdks] makale listeleri hello çeşitli dil SDK'lar, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4ef3c-272">Merhaba [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] makalede hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgulama dili .</span><span class="sxs-lookup"><span data-stu-id="4ef3c-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4ef3c-273">Merhaba [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] makale hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ef3c-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef3c-274">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ef3c-274">Next steps</span></span>
<span data-ttu-id="4ef3c-275">Cihaz çiftlerini hakkında öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="4ef3c-276">[Bir cihazda doğrudan bir yöntem çağırma][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="4ef3c-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="4ef3c-277">[Birden çok aygıta işleri zamanla][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="4ef3c-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="4ef3c-278">Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticileri aşağıdaki hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="4ef3c-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="4ef3c-279">[Nasıl toouse hello cihaz çifti][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4ef3c-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="4ef3c-280">[Nasıl toouse cihaz çifti özellikleri][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="4ef3c-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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
